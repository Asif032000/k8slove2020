# k8slove2020
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
Pods creation :
.............
podcreator.py

import os
for i in range(1,11):
    os.system('kubectl run adhoc{} --image=alpine --port 80 --command -- ping 8.8.8.8'.format(i))
 
 
 
 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
 
 
 
 /////////////////////////////////////////////////////////////////
 mailing the output :
 '
 kubectl get po,svc >> output.txt 
 
 //in the same dir create a py script :
 mail.py:
 
 import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

with open('output.txt', mode = 'r') as fp:
    msg = fp.read()

message = MIMEMultipart()
message.attach(MIMEText(msg, 'html'))
message_body = msg
sender_addr = input('Enter your e-mail ID: ')
sender_pass = input('Enter your password: ')
receiver_addr = input("Enter receiver's e-mail ID: ")



message['From'] = sender_addr
message['To'] = receiver_addr
message['Subject'] = 'SUBJECT'
message.attach(MIMEText(message_body, 'plain'))


session = smtplib.SMTP('smtp.gmail.com', 587)
session.starttls()
session.login(sender_addr, sender_pass)
text = message.as_string()
session.sendmail(sender_addr, receiver_addr, text)
session.quit()

print ('Mail Sent')
