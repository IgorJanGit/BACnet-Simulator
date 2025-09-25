# BACnet-Simulator


 QUICK START: FULL REBUILD AND RUN
# ---------------------------------
# To build all images and start all services from scratch:
#   docker compose -f simulation/bacnet-docker/docker-compose.yml down
#   docker compose -f simulation/bacnet-docker/docker-compose.yml build
#   docker compose -f simulation/bacnet-docker/docker-compose.yml up
#
# After all services are running, register the BACnet proxy/scan tool:
#   curl -X POST http://localhost:8001/start_proxy \
#     -H accept:application/json \
#     -H Content-Type:application/x-www-form-urlencoded \
#     -d local_device_address=172.25.63.101
#
# Then run Who-Is tests as described below.
#
# -----------------------------------------
# USAGE INSTRUCTIONS:
# 1. Start all services:
#      docker compose up
#
# 2. Register the BACnet proxy/scan tool with your local LAN IP (replace 172.25.63.101 with your actual LAN IP if different):
#      curl -X POST http://localhost:8001/start_proxy \
#        -H accept:application/json \
#        -H Content-Type:application/x-www-form-urlencoded \
#        -d local_device_address=172.25.63.101
#
#   Note: You can check the logs of the bacnet_scan service to see if it started successfully and is listening: 
#      docker compose logs bacnet_scan
#
# 3. Test unicast discovery (direct to device):
#      curl -X POST http://localhost:8001/bacnet/who_is \
#        -H accept:application/json \
#        -H Content-Type:application/x-www-form-urlencoded \
#        -d device_instance_low=0 \
#        -d device_instance_high=4194303 \
#        -d dest=192.168.1.141
#
# 4. Test broadcast discovery (if your network supports UDP broadcast):
#      curl -X POST http://localhost:8001/bacnet/who_is \
#        -H accept:application/json \
#        -H Content-Type:application/x-www-form-urlencoded \
#        -d device_instance_low=0 \
#        -d device_instance_high=4194303 \
#        -d dest=192.168.1.255
