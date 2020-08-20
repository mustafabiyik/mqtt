# mqtt_subscribe
import paho.mqtt.client as mqtt  # import the client
import time 
#Function to process recieved message
def process_message(client, userdata, message):
    print("message received " ,str(message.payload.decode("utf-8")))
    print("message topic=",message.topic)
    print("message qos=",message.qos)
    print("message retain flag=",message.retain)



client2 = mqtt.Client(client_id="subscriber-1") # Create client

client2.on_message = process_message # Assign callback function
broker_adress="mqtt.flespi.io"
client2.connect(broker_adress,1883,60) # Connect to broker

client2.loop_start()  # start loop to process received messages

print("subscribing ")
client2.subscribe("house/bulb1")  # subscribe
time.sleep(2)
client2.disconnect()  # disconnect
client2.loop_stop()  # stop loop
