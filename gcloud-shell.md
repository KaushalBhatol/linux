# Google Cloud shell

[Official information](https://cloud.google.com/shell/docs/accessing-cloud-shell-with-gcloud)

## Using on local terminal

### 1 google cloud sdk install

This google cloud sdk are installed in your pc.

installation:

```bash
sudo apt update && sudo apt upgrade -y

sudo apt-get install python python3 -y

curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-347.0.0-linux-arm.tar.gz

tar -xf google-cloud-sdk-*.gz

./google-cloud-sdk/install.sh 
```

## 2 Using cloud shell

1. Start a SSH session:

	gcloud cloud-shell ssh
2. Copy a file, 'data.txt', from Cloud Shell to your local machine:

	gcloud cloud-shell scp cloudshell:~/data.txt localhost:~data.txt
3. If you're using Mac or Linux, you can mount your Cloud Shell home directory onto your local file system after installing sshfs.

This allows you to edit the files in your Cloud Shell home directory using your choice of local tools. All the data in your remotely mounted file system is stored on a Persistent Disk and stored across sessions.

	gcloud cloud-shell get-mount-command ~/my-cloud-shell

