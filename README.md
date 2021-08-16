# Rotomat - Warehouse Carousel
Hanel Rotomat is a warehouse carousel where the machine itself is defined as one of the WM storage type.
This machine will be located on our premises and use Equinor network.
For any goods movement in respective warehouse managed plant, a Transfer Order (TO) is created to record in WMS.
Rotomat is defined as a separate storage type ROT with fixed bin LIFT.
Material master must be set up for rotomat storage type and bin.
Rotomat storage type will be set up in transaction OMKY to enable data send to external system.
Both TO creation and cancellation will be initiated from our system SAP.
Rotomat will respond back a confirmation to our requests.

Once the goods movement is posted, IDOC is converted to .txt using FILE setup and .txt file is placed in outbound SAP iface (AL11 directory).
Middleware system Azure Data Factory (ADF) will pick this file from iface in set time and places in their server.
Cloud server access will be granted to Hanel Rotomat and for exchange of files.
Hanel Rotomat will access this server every x seconds and picks the relevant file for TO confirmation.
Once confirmed, file will be placed back to our cloud server.
A batch job will ensure file is placed back in our inbound iface folder.
Finally a RFC call will confirm the WMTOCO IDOC and completes the process.

Flow diagram of the complete process using external storage type
![image](https://user-images.githubusercontent.com/88725237/129520821-cea7fb6a-30a9-46cc-8bd7-2156ab649e34.png)

