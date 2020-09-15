# ansible-playbooks
set of usefull ansible playbooks and roles

> Update ansible_user and ansible_password in vars.yml file to user with sudo access on the machine. You do not require asible_passwd if sudo access with NOPASSWD is set.

## Linux
### Create user with random password(gets printed in cleartext on console) and forces user to set password on first login. This doesn't do anything if user is already there.
`ansible-playbook -i hosts.ini linux/create_users.yml -K --extra-vars "username=<username> usergroup=<usergroup>"`

> This creates user with default password set as <username>. At first login user will be prompt to reset password.
> Group <usergroup> must exists


### ID Reset (password reset) to random password(gets printed in cleartext on console). Fails if user doesn't exists.
`ansible-playbook -i hosts.ini linux/reset_password.yml -K --extra-vars "username=<username>"`

### Reset Wrong Hits (Also unlocks user)
`ansible-playbook -i hosts.ini linux/reset_wronghits_and_unlock_users.yml -K --extra-vars "username=<username>"`

### Set Max Day of Password
`ansible-playbook -i hosts.ini linux/set_max_day_of_password.yml -K --extra-vars "username=<username> expiry_days=<expiry days number>"`

### Set/Change Last Password Change to Todays date
`ansible-playbook -i hosts.ini linux/update_last_password_change_date.yml -K --extra-vars "username=<username>"`

### Change account expire date (date format must be like 'Dec 1, 2020')
`ansible-playbook -i hosts.ini linux/update_account_expiry.yml -K --extra-vars "username=amna3 expiry_date='Dec 1, 2020'"`

### Set Never Expire (remove expiry from account)
`ansible-playbook -i hosts.ini linux/remove_expiry.yml -K --extra-vars "username=<username>"`

### Check Account Expiry, Password Expiry and Label
`ansible-playbook -i hosts.ini linux/check_user_status.yml -K --extra-vars "username=<username>"`

### Change label
`ansible-playbook -i hosts.ini linux/update_comment.yml -K --extra-vars "username=<username> new_label='<label>'"`

### Destroy User
`ansible-playbook -i hosts.ini linux/destroy_users.yml -K --extra-vars "username=<username>"`