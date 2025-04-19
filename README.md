Exp - 8


1.Create an EC2 instance                                                                                                          Note:Download and Save the .pem Key File and Change Key Permissions (Required by SSH).
  

 //


1. wsl --unregister Ubuntu  # Replace "Ubuntu" with your distro name if different
2.wsl  --install  (double dash)
3. Wsl.exe -d Ubuntu
4. sudo apt update
5. sudo apt install ansible -y


Move Your EC2 Key Pair (.pem) to Ubuntu 


6. mkdir -p 
7.cp /mnt/c/Users/uttek/Desktop/CC/ansible/ansible-key.pem ~/.ssh/
8. chmod 400 ~/.ssh/ansible-key.pem


9. nano inventory.ini
ubuntu@65.2.142.159(ec2public ip) ansible_ssh_private_key_file=~/.ssh/ansible-key.pem ansible_user=ubuntu


10.  nano install_nginx.yml


- name: Install and Start NGINX on EC2
  hosts: webservers
  become: yes
  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present
        update_cache: yes


    - name: Start and Enable NGINX service
      systemd:
        name: nginx
        state: started
        enabled: yes


11. ansible-playbook -i inventory.ini install_nginx.yml


12. Browse - http ec2public-ip 






~/.ssh
