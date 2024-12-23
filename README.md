# ANBERNIC RG353V Golang Development

Building apps for the [RG353V](https://anbernic.com/products/rg353v-rg353vs) using Golang.

## Hardware specifications

- CPU: RK3566 Quad-Core 64 bit Cortex-A55, Main frequency up to 1.8GHz
- RAM: LPDDR4 2GB
- Memory: 16GB TF	32GB high-speed eMMC 5.1 + 16GB TF
- Wifi/Bluetooth:	2.4/5G WIFI 802.11a/b/g/n/ac,Bluetooth 4.2

## Linux network connectivity

- Enable Wifi
  - Press the Start button
  - Move down to `Network Settings` and press the `A` button
  - Move down to `WIFI SSD`, press `A`, from the list select your WIFI ssid
  - Move down to WIFI key, enter the WIFI password, and save it
- Once Wifi is enabled and the device shows an IP the following services are available:
  - SFTP
  - SSH
  - user/pwd: root/linux

## Development with Golang

### Hello World

- In your PC open up VS Code,
- Create a golang project (`go mod init gapp1`),
- Create a `main.go` file:
- Type the following code:

```go
package main

import fmt

func main() {
  fmt.Println("Hello, World!")
}
```

- Run the app the in the PC and test it: `go run .`
- Build the app and target ARM CPU: `GOOS=linux GOARCH=arm go build -o mini main.go`
- Copy the Go application to the device: `scp gapp1 root@<DEVICE_IP>:/opt`
- Connect to the RG353V via SSH: `ssh root@<DEVICE_IP>` (defult pwd: linux)
- Run the file: `cd /opt` and `./gapp1`
- Output

```text
Hello, World!
```

## A more powerful example - run a file server

- Clone the following repo by `github.com/spcnvdr`: `git clone https://github.com/spcnvdr/go-fileserver.git`
- Navigate into the repo: `cd go-fileserver`
- Build the file server: `GOOS=linux GOARCH=arm go build -o mini main.go`
- Copy the file to the device: `scp mini root@<DEVICE_IP>:/opt`
- Connect to the RG353V via SSH from your PC: `ssh root@<DEVICE_IP>` (default pwd: linux)
- Run the file: `cd /opt` and `./mini /roms`
- Open a browser from your PC at: `http://<DEVICE_IP>:8080`
- Try to download and/or upload a file the the RG353V
- If you need more help form the `mini` app type: `mini --help`
- To exit the app and SSH
- Press CTRL+C

## Potential uses

- The RG353V is a computer on wheels and the sky here is really the limit, but some use cases are simple web services
- Raspeberry PIs and other SoCs are getting expensive, and this device offers a lot of power for a portable device
- Will look into accessing the screen and buttons, possibly to write simple utilities (like network utilities) and games
