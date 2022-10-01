import os
import pdfplumber
from pdfminer.pdfparser import PDFSyntaxError


def get_pdf_page(pdf_path):
    try:
        f = pdfplumber.open(pdf_path)
        page = len(f.pages)
    except PDFSyntaxError:
        page = 0
    return page



path = '/Users/zoser/Downloads/EMSE2'

files = []
# r=root, d=directories, f=files
for r, d, f in os.walk(path):
    for file in f:
        if '.pdf' in file:
            files.append(os.path.join(r, file))

files = sorted(files, key=lambda x: os.stat(x).st_size*-1)

for file in files:
    page_num = get_pdf_page(file)
    file_name = file.split('/')[-1].split('.')[0]

    print(f'{file_name} {file} {page_num}'' pages')
