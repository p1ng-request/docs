<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/SWIFT/SWIFT_Create_MT940_XML_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=SWIFT+-+Create+MT940+XML+file:+Error+short+description">Bug report</a>

**Tags:** #swift #mt940 #xml #file #create #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to create an MT940 XML file using Python.

<u>References:</u>
- [MT940 Format](https://www.sepaforcorporates.com/swift-for-corporates/account-statement-mt940-file-format-overview/)
- [Python XML Parser](https://docs.python.org/3/library/xml.etree.elementtree.html)

## Input

### Import libraries


```python
import xml.etree.ElementTree as ET
```

### Setup Variables
- `root`: XML root element
- `transaction`: XML transaction element
- `transaction_id`: Transaction ID
- `transaction_date`: Transaction date
- `transaction_amount`: Transaction amount


```python
root = ET.Element("MT940")
transaction = ET.SubElement(root, "Transaction")
transaction_id = "12345"
transaction_date = "2020-01-01"
transaction_amount = "1000"
```

## Model

### Create XML file

Create the XML file with the root element and the transaction element.


```python
transaction.set("id", transaction_id)
transaction.set("date", transaction_date)
transaction.set("amount", transaction_amount)
```

## Output

### Display result

Display the XML file.


```python
tree = ET.ElementTree(root)
tree.write("mt940.xml")
```

 
