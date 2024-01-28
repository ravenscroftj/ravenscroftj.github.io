public:: true

- Galaxy Tab S3 is a 10 inch (9.7") #android tablet released in 2017.
- ## TWRP
	- To install TWRP on the device it's best to use [this chap's release](https://forum.xda-developers.com/t/recovery-unofficial-sm-t820-sm-t825-2021-11-30-twrp-3-6-0_9-0-for-galaxy-tab-s3.4303163/) and install via Heimdall:
	- `apt-get install heimdall-flash`
	- Once you have the files ready to go, put the tablet into download mode with Power + Vol Down + Home (hold for 10 seconds).
	- ```shell
	  heimdall flash --RECOVERY ./Downloads/twrp-3.6.0_9-0-gts3lwifi.img --no-reboot
	  ```
	- It's important to now reboot straight into recovery so that the old recovery partition is not recovered - Power + Vol Up + Home
	- Swipe to install TWRP
- ## LineageOS
	- Use LineageOS 19 [this release](https://forum.xda-developers.com/t/rom-unofficial-12l-eas-sm-t820-sm-t825-2022-07-15-lineageos-19-1-for-galaxy-tab-s3.4418855/) is most stable
	- Using [NikGApps](https://nikgapps.com/downloads#downloads) 12.1 (SL)
	- From TWRP install the zip files.