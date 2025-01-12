# QR Code Generator with Jupyter Notebook

This project demonstrates how to create a QR code using Python in a Jupyter Notebook. The steps below guide you through setting up the environment, installing required libraries, and generating the QR code.

## Prerequisites
- Python 3 installed on your system.
- Basic understanding of Python programming.

---

## Steps

### 1. Navigate to your workspace
Run the following command to navigate to your workspace directory:
```bash
cd /home/raptor/workspace/jupyter
```

### 2. Create a virtual environment
Create an isolated Python environment to avoid conflicts with system-wide libraries:
```bash
python3 -m venv venv
```
This will create a folder named `venv` in your current directory containing the virtual environment files.

### 3. Activate the virtual environment
Activate the virtual environment with the following command:
```bash
source venv/bin/activate
```
You should see the virtual environment name (e.g., `(venv)`) appear in your terminal prompt.

### 4. Install Jupyter
Install Jupyter Notebook, which will be used to write and run Python code:
```bash
pip3 install jupyter
```

### 5. Install necessary libraries
Install the libraries required for generating QR codes:
```bash
pip3 install qrcode Pillow
```
- **qrcode**: Used for generating QR codes.
- **Pillow**: A Python Imaging Library for creating and manipulating images.

### 6. Launch Jupyter Notebook
Start Jupyter Notebook to write your Python code:
```bash
jupyter notebook
```
This command will open the Jupyter Notebook interface in your web browser. Create a new Python notebook and add the following code to generate a QR code:
```python
import qrcode

def generate_vcard_qr(
    first_name,
    last_name,
    organization,
    position,
    phone,
    email,
    website,
    street,
    zip_code,
    city,
    state,
    country,
    file_name="vcard_qr.png"
):
    """
    Generate a QR code for a vCard and save it as an image.

    :param first_name:    Contact's first name
    :param last_name:     Contact's last name
    :param organization:  Contact's organization/company
    :param position:      Contact's position/work title
    :param phone:         Contact's phone number
    :param email:         Contact's email address
    :param website:       Contact's website URL
    :param street:        Street address
    :param zip_code:      Zip/postal code
    :param city:          City
    :param state:         State/region
    :param country:       Country
    :param file_name:     Name of the file to save the QR code image
    """

    # vCard 3.0 format
    # ADR is: ADR;TYPE=WORK,PREF:;;Street;City;State;Zip;Country
    vcard_data = (
        "BEGIN:VCARD\n"
        "VERSION:3.0\n"
        f"N:{last_name};{first_name};;;\n"
        f"FN:{first_name} {last_name}\n"
        f"ORG:{organization}\n"
        f"TITLE:{position}\n"
        f"TEL;TYPE=WORK,VOICE:{phone}\n"
        f"EMAIL;TYPE=INTERNET:{email}\n"
        f"URL;TYPE=WORK:{website}\n"
        f"ADR;TYPE=WORK,PREF:;;{street};{city};{state};{zip_code};{country}\n"
        "END:VCARD"
    )

    # Create the QR code
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_L,  # Lower error correction
        box_size=10,
        border=4,
    )
    qr.add_data(vcard_data)
    qr.make(fit=True)

    # Generate the QR code image
    img = qr.make_image(fill_color="black", back_color="white")
    img.save(file_name)
    print(f"QR code saved to {file_name}")


if __name__ == "__main__":
    # Example usage
    generate_vcard_qr(
        first_name="John",
        last_name="Doe",
        organization="Acme Inc.",
        position="Software Developer",
        phone="+1234567890",
        email="john.doe@example.com",
        website="https://www.example.com",
        street="123 Main Street",
        zip_code="12345",
        city="Springfield",
        state="Illinois",
        country="USA",
        file_name="john_doe_vcard.png"
    )

```

### 7. Deactivate the virtual environment
Once you are done, deactivate the virtual environment:
```bash
deactivate
```
This will return your terminal to the global Python environment.

---

## Notes
- Ensure that `venv` is activated before running commands to install libraries or launch Jupyter Notebook.
- The generated QR code will be saved as `qrcode.png` in the current working directory.

---

## Common Mistakes
1. **Misspelled commands**:
   - Ensure proper syntax for commands, e.g., `pip3 install`, not `pip install3`.
2. **Virtual environment not activated**:
   - Always activate the virtual environment using `source venv/bin/activate` before running Python commands.
3. **Wrong directory**:
   - Run `cd /home/raptor/workspace/jupyter` before creating the virtual environment to ensure you are in the correct workspace.

By following these steps, you will successfully create a QR code using Python and Jupyter Notebook.
