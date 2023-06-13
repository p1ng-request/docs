<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PDF/PDF_Transform_to_MP3.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=PDF+-+Transform+to+MP3:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pdf #text2audio #snippet #operations #mp3

**Author:** [Sanjay Sabu](https://www.linkedin.com/in/sanjay-sabu-4205/)

**Description:** This notebook converts PDF documents into MP3 audio files.

## Input

### Installing necessary packages


```python
!pip install pdfminer.six
```


```python
!pip install gTTS
```

### Import library


```python
from io import StringIO
from pdfminer.converter import TextConverter
from pdfminer.layout import LAParams
from pdfminer.pdfdocument import PDFDocument
from pdfminer.pdfinterp import PDFResourceManager, PDFPageInterpreter
from pdfminer.pdfpage import PDFPage
from pdfminer.pdfparser import PDFParser
from gtts import gTTS
```

## Model

### Function to convert pdf  file to text


```python
def convert_pdf_to_string(file_path):

    output_string = StringIO()
    with open(file_path, "rb") as in_file:
        parser = PDFParser(in_file)
        doc = PDFDocument(parser)
        rsrcmgr = PDFResourceManager()
        device = TextConverter(rsrcmgr, output_string, laparams=LAParams())
        interpreter = PDFPageInterpreter(rsrcmgr, device)
        for page in PDFPage.create_pages(doc):
            interpreter.process_page(page)

    return output_string.getvalue()


def convert_title_to_filename(title):
    filename = title.lower()
    filename = filename.replace(" ", "_")
    return filename


def split_to_title_and_pagenum(table_of_contents_entry):
    title_and_pagenum = table_of_contents_entry.strip()

    title = None
    pagenum = None

    if len(title_and_pagenum) > 0:
        if title_and_pagenum[-1].isdigit():
            i = -2
            while title_and_pagenum[i].isdigit():
                i -= 1

            title = title_and_pagenum[:i].strip()
            pagenum = int(title_and_pagenum[i:].strip())

    return title, pagenum
```

## Output

### Content


```python
pdf_name = "Installation_Guide.pdf"  # .pdf file you want to convert
print(convert_pdf_to_string(pdf_name))
```

### Converting to mp3


```python
rr = convert_pdf_to_string(pdf_name)
string_of_text = ""
for text in rr:
    string_of_text += text

final_file = gTTS(text=string_of_text, lang="en")  # store file in variable
final_file.save("Generated Speech.mp3")  # save file to computer
```
