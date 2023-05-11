# kumbio-automation

# English
# To use this: 
1. Install Ansible agent:
   1. https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#pip-install
   2. Clone this repository to your local machine `git clone git@github.com:HenrySpartGlobal/kumbio-automation.git`

## Connect with ansible
1. On your local machine, navigate to your project directory (where the kumbio-automation directory is located), and generate a new SSH key pair:
   1. `ssh-keygen -t rsa -b 4096 -f ansible/privatekey/your_key_name -C "kumbio-prod"`
2. Copy the public key to your server:
   1. `ssh-copy-id -i ansible/privatekey/your_key_name.pub root@[IP]`
   2. Replace `your_key_name` with the name you used in the previous step, and replace [IP] with your server's IP address. This command will append the public key to the `~/.ssh/authorized_keys` file on your server for the root user.
3.Update your `inventories/local.ini` inventory file to use the new private key:

```
[dev]
ansible_user=root ansible_ssh_private_key_file=ansible/privatekey/your_key_name
```
 
4. Replace your_key_name with the name you used in step 1.
5. Now you should be able to run the Ansible playbook using the new SSH key pair for authentication:
   1. `ansible-playbook -i ansible/inventories/local.ini ansible/playbooks/ping_test.yml`

6. If everything is set up correctly, the playbook should run successfully, and the server should respond to the ping using the new private key for authentication.

## Setup Kumbio server
This will run the script on the server to automatically setup kumbio server and install docker
1. `ansible-playbook -i ansible/inventories/local.ini ansible/playbooks/setup.yml --vault-id secrets@ansible/secrets/vault_password.txt --ask-become-pass`
   1. When asked about `BECOME password: ` enter the SSH password for the server. 
2. This will run the ansible and create a user kumbio, and install docker. 
3. You can now log in with `ssh kumbio@[IP]`
4. You will then be prompted with a password - This should have been provided by Henry
5. You may also change this password of the user, please contact Henry for the instructions for this.


# Spanish
# Para usar esto:
1. Instala el agente de Ansible:
   1. https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#pip-install
   2. Clona este repositorio en tu máquina local `git clone git@github.com:HenrySpartGlobal/kumbio-automation.git`

## Conectar con Ansible
1. En tu máquina local, navega hasta el directorio de tu proyecto (donde se encuentra el directorio kumbio-automation) y genera un nuevo par de claves SSH:
   1. `ssh-keygen -t rsa -b 4096 -f ansible/privatekey/nombre_de_tu_clave -C "kumbio-prod"`

2. Copia la clave pública a tu servidor:
`ssh-copy-id -i ansible/privatekey/nombre_de_tu_clave.pub root@[IP]`
Reemplaza `your_key_name` con el nombre que usaste en el paso anterior, y reemplaza [IP] con la dirección IP de tu servidor. Este comando añadirá la clave pública al archivo `~/.ssh/authorized_keys` en tu servidor para el usuario root.

3. Actualiza tu archivo de inventario `inventories/local.ini` para usar la nueva clave privada:
```
[dev]
ansible_user=root ansible_ssh_private_key_file=ansible/privatekey/your_key_name
```

4. Reemplaza nombre_de_tu_clave con el nombre que usaste en el paso 1.
5. Ahora deberías ser capaz de ejecutar el playbook de Ansible utilizando el nuevo par de claves SSH para la autenticación:

   1. `ansible-playbook -i ansible/inventories/local.ini ansible/playbooks/ping_test.yml`
6. Si todo está configurado correctamente, el playbook debería ejecutarse con éxito, y el servidor debería responder al ping utilizando la nueva clave privada para la autenticación.

## Configura el servidor Kumbio
Esto ejecutará el script en el servidor para configurar automáticamente el servidor Kumbio e instalar Docker.
1. `ansible-playbook -i ansible/inventories/local.ini ansible/playbooks/setup.yml --vault-id secrets@ansible/secrets/vault_password.txt --ask-become-pass`
   1. Cuando te pregunte sobre `BECOME password:` introduce la contraseña SSH para el servidor.

2. Esto ejecutará el ansible, creará un usuario kumbio e instalará docker.
3. Ahora puedes iniciar sesión con `ssh kumbio@[IP]`
4. Se te pedirá una contraseña - Esta debería haber sido proporcionada por Henry
5. También puedes cambiar esta contraseña del usuario, por favor, contacta a Henry para las instrucciones de esto.
