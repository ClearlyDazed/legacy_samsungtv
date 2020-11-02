# legacy_samsungtv
Home Assistant Integration for legacy Samsung TV.

The samsungtv platform allows you to control a Samsung Smart TV.

Setup
Go to the integrations page in your configuration and click on new integration -> Samsung TV. If your TV is on and you have enabled SSDP discovery, it's likely that you just have to confirm the detected device.

When the TV is first connected, you will need to accept Home Assistant on the TV to allow communication.

YAML Configuration
YAML configuration is around for people that prefer YAML. To use this integration, add the following to your configuration.yaml file:

# Example configuration.yaml entry
samsungtv:
  - host: IP_ADDRESS
{% configuration %} host: description: "The hostname or IP of the Samsung Smart TV, e.g., 192.168.0.10." required: true type: string name: description: The name you would like to give to the Samsung Smart TV. required: false type: string turn_on_action: description: "Defines an action to turn the TV on." required: false type: list {% endconfiguration %}

After saving the YAML configuration, the TV must be turned on before launching Home Assistant in order for the TV to be registered the first time.

Wake up TV
To wake up the TV when switched off you can use the wake-on-lan integration and call a service. This is not possible with every device.

wake_on_lan:

samsungtv:
  - host: IP_ADDRESS
    turn_on_action:
      - service: wake_on_lan.send_magic_packet
        data:
          mac: "11:22:33:44:55:66"
Usage
Changing channels
Changing channels can be done by calling the media_player.play_media service with the following payload:

entity_id: media_player.samsung_tv
media_content_id: 590
media_content_type: channel
Selecting a source
It's possible to switch between the 2 sources TV and HDMI.

Home Assistant Core additional requirements
You will need to install the websocket-client Python package in your Home Assistant install. This will probably be done with:

pip3 install websocket-client
Remembering to activate your venv if you're using a venv install.
