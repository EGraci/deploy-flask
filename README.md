# deploy-flask with nginx and gunicorn

## Install Requirement
```
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
```

## Settings Env Python
Tutorial <a href="https://flask.palletsprojects.com/en/latest/deploying/gunicorn/">Link</a>
Genrate env
```
python -m venv venv
```
Running env
```
. .venv/bin/activate
```
Install application support
```
pip install .  //install your application support
pip install flask
pip install gunicorn
```
Testing Gunicorn
```
gunicorn -w 4 '[nameFile.py]:app'
```
Adding file wsgi.py
```
from [nameFile.py] import app

if __name__ == "__main__":
    app.run()
```
Testing again wiht defaul 0.0.0.0
```
gunicorn --bind 0.0.0.0:8000 wsgi:app
```
Exiting env
```
deactivate
```

## Settings systemctl
create new file
```
nano /etc/systemd/system/[nameFileSystem.service]
```
Inside file
```
Description= //decription up to you
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/[path env]
Environment="PATH=/[path env]/venv/bin"
ExecStart=/[path env]/venv/bin/gunicorn --workers 3 --bind unix:sispakde.sock -m 007 wsgi:app

[Install]
WantedBy=multi-user.target
```
Start sytemctl
```
sudo systemctl start [nameFileSystem] 
sudo systemctl enable [nameFileSystem] 
sudo systemctl status [nameFileSystem] 
```
