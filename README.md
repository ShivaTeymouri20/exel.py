import json
import pandas as pd


customer_data = {
    "customers": [
        {"name": "Ali Ahmadi", "phone": "09123456789", "email": "ali@gmail.com"},
        {"name": "Sara Karimi", "phone": "09119876543", "email": "sara@gmail.com"},
        {"name": "Reza Moradi", "phone": "09351234567", "email": "reza@gmail.com"}
    ]
}


with open("customers.json", "w") as json_file:
    json.dump(customer_data, json_file, indent=4)


def export_to_excel(json_file, output_excel, fields):

    with open(json_file, "r") as file:
        data = json.load(file)


    customers = data["customers"]


    filtered_data = [{field: customer[field] for field in fields} for customer in customers]


    df = pd.DataFrame(filtered_data)


    df.to_excel(output_excel, index=False)
    print(f"فایل اکسل با موفقیت ذخیره شد: {output_excel}")



selected_fields = ["name", "phone"]


export_to_excel("customers.json", "customer_contacts.xlsx", selected_fields)
