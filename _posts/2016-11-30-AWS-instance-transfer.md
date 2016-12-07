---
layout: single
title: Transfer AWS instance with different region and different account
tags: [aws]
date: 2016-11-30 00:00
---
Check the speed of each region on `http://www.cloudping.info/`.
AccountA: has the original instance in **N. Virginia**
AccountB: will create instance in **Singapore**

# Steps
1. Login [https://console.aws.amazon.com/console/home][1] with AccountA;
2. Find your EC2 instance in **N. Virginia**
3. Select your instance and click `Actions` \> `Image` \> `Create Image`;
4. Set the only required field `Image name`, let others default, click `Create Image`;
5. Wait for a moment, you will find `AMI` and `Snapshot` created;
6. Click `IMAGES` \> `AMIs` \> `Actions` \> `Copy AMI`;
7. Select **Asia Pacific (Singapore)** in `Destination region` and click `Copy AMI`;
8. Wait for a moment and change your region to ** Singapore** , find the new Image under `IMAGES` \> `AMIs`, copy the `AMI ID`;
9. Click `Actions` \> `Modify Image Permissions`;
10. Set AccountB number and click `Add Permission` to make this Image available to AccountB;
11. Logout AccountA and login AccountB;
12. Change your region to **Singapore**,  move to EC2 page and click `Launch Instance`;
13. Search the copied `AMI ID` under `Community AMIs`;
14. that’s all.

[1]:	https://console.aws.amazon.com/console/home