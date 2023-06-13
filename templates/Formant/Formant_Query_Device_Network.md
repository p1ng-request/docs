<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Formant/Formant_Query_Device_Network.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Formant+-+Query+Device+Network:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #formant #matplotlib #notification #email #image

**Author:** [Nicolas Binford](https://www.linkedin.com/in/nicolasbinford)

**Description:** This notebook queries network data over a period of time from a Formant device, graphs it, and emails the images.

**Reference:** 
- https://docs.formant.io/

## Input

### Install packages


```python
!pip install formant
```

### Import libraries


```python
from datetime import datetime, timedelta
import dateutil.parser as parser
import numpy as np
import matplotlib.pyplot as mplt
import os

# Comment out this and Part 3 if running outside of Naas
import naas

from formant.sdk.cloud.v2 import Client as FormantClient
from formant.sdk.cloud.v2.formant_admin_api_client.models.device_query import (
    DeviceQuery,
)
from formant.sdk.cloud.v2.formant_admin_api_client.models.event_query import (
    EventQuery,
    EventQueryEventTypesItem,
    EventQuerySeveritiesItem,
)
from formant.sdk.cloud.v2.formant_admin_api_client.models.event_list_response import (
    EventListResponse,
)
from formant.sdk.cloud.v2.formant_query_api_client.models.query import Query
```

### Setup Variables


```python
# Service account with "viewer" role
FORMANT_EMAIL_DEMO = "naas-demo@0d29f656-cc1c-4b9e-baad-199cfa1fcced.iam.formant.io"
FORMANT_PASSWORD_DEMO = "prHHR_nnpzre3ZYTEZJ-NFGfS6OKRiEXw8xiJqtmlFuAT1Jx6yFyVQLmFe_ig9ei"

# 10 hours of data
START_TIME = "2023-03-10T00:00:00.000Z"
END_TIME = "2023-03-10T00:10:00.000Z"

# Put your email address here
EMAIL_TO=["nicolas@formant.io", "jeremy@naas.ai"]
```

## Model

### Query and work with Formant data


```python
"""
Part 1: Query from Formant
"""

# Names of devices you want to query
my_device_names = ["walter"]

# Streams that you want to query
streams_of_interest = [
    "$.host.network",
]

# Set up API clients
fclient = FormantClient(email=FORMANT_EMAIL_DEMO, password=FORMANT_PASSWORD_DEMO)
admin_api = fclient.admin
query_api = fclient.query

# Get a list of all available devices
# Store device_id of desired devices, which is what is used for querying
device_ids_to_query = []
device_query = DeviceQuery(enabled=True)
response = admin_api.devices.query(device_query).parsed
for device in response.items:
    if device.name in my_device_names:
        device_ids_to_query.append(device.id)

# Specify timerange for which script should pull data
start = parser.isoparse(START_TIME)
end = parser.isoparse(END_TIME)

# The final list with the data from each device
device_data_dicts = []

for device_id in device_ids_to_query:
    # Dict structure:
    # {device: {data_label_0: [values], data_label_1: [values],...}}
    device_data_dict = {}
    data_values = {}

    # Query stream data for this device
    for stream_name in streams_of_interest:
        query_model = Query(
            start=start,
            end=end,
            device_ids=[device_id],
            names=[stream_name],
        )
        response = query_api.queries.query(query_model)
        response_items = response.parsed.items

        # Labels specific to your desired stream
        event_data_labels = ["transmit", "receive"]
        for label in event_data_labels:
            data_values[label] = []

        for item in response_items:
            # Some streams have 1 "item" with multiple "points", some have
            # multiple "items" with multiple "points"
            item_points = item.points
            for point in item_points:
                # This the entire datapoint with multiple labels and values
                event_data = point.additional_properties["value"][1]
                for datapoint_specific in event_data:
                    if datapoint_specific["label"] in data_values.keys():
                         datapoint_specific_label = datapoint_specific["label"]
                         datapoint_specific_value = datapoint_specific["value"]
                         data_values[datapoint_specific_label].append(datapoint_specific_value)

    # Build the final dict structure
    device_data_dict[device_id] = data_values
    # Add the dict to the final list
    device_data_dicts.append(device_data_dict)

"""
Part 2: Working with the data
"""
attachments = []
#attachments = ""
attachment_number = 0

for device_data_dict in device_data_dicts:
    # This is the device
    device_id = list(device_data_dict.keys())[0]
    # This is all of the data for that device
    for data_values in device_data_dict.values():
        # This is each type of event label in that datapoint
        for datapoint_specific_label in data_values:

            # This is the list of data from each stream
            y_axis = np.asarray(data_values[datapoint_specific_label])
            num_datapoints = len(y_axis)
            # Create time increments for X-axis
            x_axis = []
            increment = (end - start) / num_datapoints
            for i in range(0, num_datapoints):
                x_axis.append(start + (increment * i))

            # Plot the data
            mplt.figure(f"Formant Query Results {attachment_number}", figsize=(14, 10))
            mplt.plot(x_axis, y_axis)
            # Hardcode some things for the labels text, but could make more generic
            title = (f"Device: {device_id}\n" +
                    f"Network {datapoint_specific_label} (Mbps)\n" +
                    f"{start} to {end}")
            mplt.title(title)
            max_value = np.amax(y_axis)
            avg_value = np.average(y_axis)
            mplt.xlabel(f"\nMax value: {max_value}\nAverage value: {avg_value}", fontsize=14)
            outfile_name = f"figure_{attachment_number}.png"
            mplt.savefig(outfile_name)
            outfile_path = os.path.join(os.getcwd(), outfile_name)
            attachments.append(outfile_path)
            attachment_number += 1
```

## Output

### Send results to email


```python
"""
Part 3: Exporting the data
"""
email_subject = f"Formant Query Result, {datetime.now()}"
naas.notification.send(
    email_to=EMAIL_TO,
    subject=email_subject,
    html="<p>Hello from Formant! Here is the data you requested.<p>",
    files=attachments
)
```
