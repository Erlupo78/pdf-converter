import streamlit as st
import PyPDF2
import pandas as pd
from io import BytesIO

st.title("PDF to Excel Converter")

uploaded_file = st.file_uploader("Upload a PDF file", type=["pdf"])

if uploaded_file is not None:
    reader = PyPDF2.PdfReader(uploaded_file)

    extracted_text = []
    for i, page in enumerate(reader.pages):
        text = page.extract_text()
        extracted_text.append({"Page": i + 1, "Content": text})

    df = pd.DataFrame(extracted_text)

    # Convert DataFrame to Excel in memory
    output = BytesIO()
    with pd.ExcelWriter(output, engine="openpyxl") as writer:
        df.to_excel(writer, index=False, sheet_name="PDF_Text")

    st.success("Conversion complete!")

    st.download_button(
        label="Download Excel File",
        data=output.getvalue(),
        file_name="pdf_converted.xlsx",
        mime="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
    )
