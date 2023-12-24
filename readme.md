# IOT
Gateway for IOT application using Docker containers: timescaleDB, node-red, Grafana

## To-do:
1. Define phone numbers in database
2. Send Whatsapp to list of numbers
3. Connect to DGA
4. Phone numbers and API key on environment variables.

## Mounting docker containers
### Docker compose
1. Go to project docker folder: ```cd /home/pi/IOT```
2. Check that Grafana has defined userid to 1000.
3. [Add login to node-red](https://nodered.org/docs/user-guide/runtime/securing-node-red):
    * Enter node-red cointainer: ```docker exec -it nodered /bin/bash```
    * Edit /data/settings.js file: ```nano /data/settings.js```
4. Run initialization of containers: ```docker compose up -d```

## Github commands
1. Clone repository: ```git clone -b main https://github.com/r9hino/ACM.git```
2. Github commit:
    * ```git add .```
    * ```git commit -m "Description"```
    * ```git push origin main```

## Backup Ubuntu OS while running
### Mount storage device
1. Create mounting point: ```mkdir /mnt/SD```
2. Check if device was detected and what is it partition: ```lsblk```
3. Mount the device: ```sudo mount /dev/sda1 /mnt/SD```
4. Check if device was correctly mounted: ```lsblk```
### Make an Ubuntu image and store it on the mounted device
1. Download [PiSafe](https://github.com/RichardMidnight/pi-safe):
    * ```wget https://raw.githubusercontent.com/RichardMidnight/pi-safe/main/pisafe -O pisafe```
    * ```bash pisafe install```
2. Stop all processes:
    * ```pm2 stop all```
    * ```cd /home/pi/Code/ACM/Docker```
    * ```docker-compose -f docker-nodered-influxdb-pigpiod.yml --env-file ./../.env stop```
3. Run PiSafe: ```pisafe```
4. On Settings turn off "hide root device"
5. Go to Backup
6. Choose Ubuntu OS partition
7. Set destination path to /mnt/SD
8. After finishing the image creation, unmount device: ```sudo umount /mnt/SD```
9. Check unmounting: ```lsblk```
