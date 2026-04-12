## Checks Before Installation
- Ensure VM's OS is Ubuntu 22.0
- Ensure Both VM's are on same network (VPC for Amazon , VNET for Azure)
- If on Amazon Add a Inbound port rule for **All Traffic** from the **security-group** of Agent
- Better to Keep all Machines in Same **security-group**
- 
- Make sure You are able to ping VM's from each other  
Example
```sh
ping <Other-VM-Private-IP>
```

- Security Group Should look like this
<img width="1190" height="651" alt="image" src="https://github.com/user-attachments/assets/e40ba53b-0cca-414b-979e-c32714036f76" />

## Step-1
<img width="1908" height="795" alt="image" src="https://github.com/user-attachments/assets/87235708-f610-4c5f-9ea4-9be7ccc45173" />

## Step-2
- Use t3.small to handle the things smoothly.
- Create one pem key and use the same key for every instance.
<img width="1919" height="814" alt="image" src="https://github.com/user-attachments/assets/2773f4cd-2293-4d5e-9cb1-2918034da38e" />

## Step-3
- Use same network settings for all the instances.
- Create one security group, like showed in the starting and use that security group only for every instance.
<img width="1918" height="766" alt="image" src="https://github.com/user-attachments/assets/8aac47de-1aee-4c76-8cad-ebd3f638091b" />

## In the same way create both the instances. 
