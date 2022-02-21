## List of known public services

* Ask on one of the following rooms: #mautrix_yunohost:matrix.fdn.fr or #googlechat:maunium.net

## Bridging usage
** Note that several Google Chat and Matrix users can be bridged, each Google Chat account has its own bot administration room. If they are in a same Google Chat group, only one matrix room will be created. **

### Bridge a Google Chat user and a Matrix user
* First your Matrix user or Synapse Server has to be authorized in the Configuration of the bridge (see below)
* Then, invite the bot (default @googlechatbot:yoursynapse.domain) in this new Mautrix-Google Chat bot administration room.
  * If the Bot does bot accept, see the [troubleshooting page](https://docs.mau.fi/bridges/general/troubleshooting.html)
* Send ``!gc help`` to the bot in the created room to know how to control the bot.
See also [upstream wiki Authentication page](https://docs.mau.fi/bridges/python/googlechat/authentication.html)

#### Linking the Bridge as a secondary device
* Type ``!gc link``
* Open Google Chat App of your primary device
* Open Settings => Linked Devices => + => Capture the QR code with the camera
* By defaults, only conversations with very recent messages will be bridged
* Accept invitations to the bridged chat rooms

#### Registering the Bridge as a primary device
* Type ``!gc register <phone>``, where ``<phone>`` is your phone number in the international format with no space, e.g. ``!gc register +33612345678``
* Answer in the bot room with the verification code that you reveived in SMS.
* Set a profile name with ``!gc set-profile-name <name>``

### Double puppeting
* Log in with ``login-matrix <access token>``
* After logging in, the default Matrix puppet of your Google Chat account should leave rooms and your account should join all rooms the puppet was in automatically.


### Relaybot: Bridge a group for several Matrix and several Google Chat users to chat together
* Create a room on the googlechat side
* Your bridged users will be invited on the Matrix side once they are invited on the Google Chat side
* You can invite more people over on the Matrix side
* Have one of the bridged users (who has the right permission) type `!gc set-relay` on the Matrix side. Their googlechat account will relay messages from other Matrix users
It is not yet possible to bridge to an existing googlechat room, or create a new googlechat room from the Matrix side.

## Configuration of the bridge

The bridge is [roughly configured at installation](https://github.com/YunoHost-Apps/mautrix_googlechat_ynh/blob/master/conf/config.yaml), e.g. allowed admin and user of the bot. Finer configuration can be done by modifying the
following configuration file with SSH: 
```/opt/yunohost/mautrix_googlechat/config.yaml```
and then restarting the mautrix_googlechat service.

## Documentation

 * Official "Mautrix-Google Chat" documentation: https://docs.mau.fi/bridges/python/googlechat/index.html
 * Matrix room (Matrix Bridges in Yunohost): #mautrix_yunohost:matrix.fdn.fr
 * Matrix room (upstream app): #googlechat:maunium.net
In case you need to upload your logs somewhere, be aware that they contain your contacts' and your phone numbers. Strip them out with 
``| sed -r 's/[0-9]{10,}/📞/g' ``
 * YunoHost documentation: If more specific documentation is needed, feel free to contribute.

## YunoHost specific features

#### Multi-user support

* Bot users are not related to Yunohost users. Any Matrix account or Synapse server autorized in the configuration of the bridge can invite/use the bot. 
* The Google Chat bot is a local Matrix-Synapse user, but accessible through federation (synapse public or private).
* Several Google Chat and Matrix users can be bridged with one bridge, each user has its own bot administration room. 
* If several bot users are in a same Google Chat group, only one Matrix room will be created by the bridge.
* See https://github.com/YunoHost-Apps/synapse_ynh#multi-users-support

#### Multi-instance support

* Multi-instance installation should work. Several bridge instances could be installed for one Matrix-Synapse instance so that one Matrix user can bridge several Google Chat accounts. 
* Several bridge instances could be installed for each Matrix-Synapse instance to benefit from it. But one bridge can be used by users from several Matrix-Synapse instances.

## Limitations

* It looks like media are not bridged. 
* Google Chat chats are not grouped in a Matrix community (as opposed to the Mautrix-WhatsApp or Mautrix-Facebook bridges)