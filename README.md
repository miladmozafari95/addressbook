import csv


contacts=[]

def save_contacts():
    with open('addressbook.csv', 'w', newline='') as file:
        Headre_name=['Name', 'Phone', 'Email', 'Address']
        writer=csv.DictWriter(file, fieldnames=Headre_name)
        writer.writeheader
        writer.writerows(contacts)

def view_contacts():
    print('Your Address Book:')
    for contact in contacts:
        print(f"Name: {contact['Name']}")
        print(f"Phone: {contact['Phone']}")
        print(f"Email: {contact['Email']}")
        print(f"Address: {contact['Address']}")
        print('-' * 30)
        

def add_contact():
    print('Add New Contact:')
    name=input('Name: ')
    phone=input('Phone: ')
    email=input('Email: ')
    address=input('Address: ')

    if not phone.isdigit():
        raise ValueError('Phone number must be numeric')
    
    contact={'Name':name, 'Phone':phone, 'Email':email, 'Address':address}
    contacts.append(contact)
    save_contacts()
    print(f'{name} has been added to your contacts')

def update_contact():
    print('update a contact')
    phone=input('enter the phone number of the contact to update: ')
    if not phone.isdigit():
        raise ValueError('Phone number must be numeric')
    for contact in contacts:
        if contact['Phone'] == phone:
            print(f'Current Details for {contact["Name"]}:')
            print(f'Name: {contact["Name"]}')
            print(f'Phone: {contact["Phone"]}')
            print(f'Email: {contact["Email"]}')
            print(f'Address: {contact["Address"]}')
            print('-' * 30)

            new_name=input('New Name (press Enter to Keep Current): ').strip()
            new_email=input('New Name (press Enter to Keep Current): ').strip()
            new_address=input('New Name (press Enter to Keep Current): ').strip()

            if new_name:
                contact['Name']=new_name
            elif new_email:
                contact['Email']=new_email
            elif new_address:
                contact['Address']=new_address
            save_contacts()
            print(f"contact details for {contact['Name']} has been updated")
            return
    print('contact not found')    

def delete_contact():
    print('delete a contact')
    phone=input('enter the phone number of the contact to delete: ')
    if not phone.isdigit():
        raise ValueError('Phone number must be numeric')
    
    for contact in contacts:
         if contact['Phone'] == phone:
             deleted_name=contact['Name']
             contacts.remove(contact)
             save_contacts()
             print(f"{deleted_name} has been deleted from your address book")
             return
    print('contact not found')    


def open_file():
    try:
        with open('addressbook.csv', 'r') as file:
            lines=csv.DictReader(file)
            for line in lines:
                contacts.append(line)
    except FileNotFoundError:
        print('This File does not Exist')

open_file()
while True:
    try:
        print()
        print('your address book menu:')
        print('1. Add contact')
        print('2. view contact')
        print('3. Update contact')
        print('4. Delete contact')
        print('5. Exit')

        choice= int(input('Enter your choice(1/2/3/4/5): ').strip())

        if choice==1:
            add_contact()
        elif choice==2:
            view_contacts()
        elif choice==3:
            update_contact()
        elif choice==4:
            delete_contact()
        elif choice==5:
            print('Goodbye')
            exit()
        else:
            print('Invalid choice! please try again')
    except Exception as e:
        print(f'Error: {e}')


