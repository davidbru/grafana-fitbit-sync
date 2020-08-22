# REQUIREMENTS

## Direnv
- Creates folder based environment variables which can be defined in ./.envrc 
- Installation: https://direnv.net/#basic-installation
- After every change of the .envrc file you need to allow the changes with the command
    ```
    $ direnv allow .
    ```
- Test env variables in python
    ```
    import os
    print ("test1: %s" % os.environ.get('DB_HOST'))
    print ("test2: %s" % os.environ.get('CLIENT_SECRET'))
    ```


## Virtual Environment
- First installation
    ```
    $ python3 -m venv python-venv
    ```
- Change into virtual environment
    ```
    $ source python-venv/bin/activate
    ```
- Install python dependencies
    ```
    $ pip3 install python-dateutil fitbit influxdb
    ```
- Write requirements.txt for reinstallation (optional)
    ```
    $ pip freeze > requirements.txt
    $ pip install -r requirements.txt
    ```
- Deactivate venv
    ```
    $ deactivate
    ```


## GRAFANA Dashboard
- https://grafana.com/grafana/dashboards/12348


## Fitbit API Exporter
- https://gitlab.com/fsvm88/fitbit-api-exporter
- Use only api_poller.py
- Diff Changes
    ```
    170,171c170,171
    <         'elevation': None,  # dateTime, value
    <         'floors': None,  # dateTime, value
    ---
    > #        'elevation': None,  # dateTime, value
    > #        'floors': None,  # dateTime, value
    187,188c187,188
    <         'elevation',  # dateTime, value
    <         'floors',  # dateTime, value
    ---
    > #        'elevation',  # dateTime, value
    > #        'floors',  # dateTime, value
    212,215c212,215
    <     'foods_log': [
    <         'caloriesIn',
    <         'water'
    <     ],
    ---
    > #    'foods_log': [
    > #        'caloriesIn',
    > #        'water'
    > #    ],
    ```


## Service
- /lib/systemd/system/fitbit.service
    ```
    [Unit]
    Description=Fitbit Data Import
    After=multi-user.target
    
    [Service]
    Type=idle
    ExecStart=/home/plex/Documents/Scripts/fitbit/scripts/api_poller-CLI.sh > /tmp/fitbit-log.txt 2>&1
    
    [Install]
    WantedBy=multi-user.target
    ```
- `sudo systemctl daemon-reload`
- `sudo systemctl enable fitbit.service`
- `sudo systemctl start fitbit.service`
- `sudo systemctl status fitbit.service`
- `sudo systemctl stop fitbit.service`
- `sudo systemctl disable fitbit.service`