---
layout: post
title: Neural Style on AWS GPU Instance!
image: /img/hello_world.jpeg
comments: true
tags: [aws, jupyter-notebook, cnn]
mathjax: true
---

This is my example of running a jupyter notebook on an AWS GPU instance. This allows us to greatly speed up all the computations while having all the convenience of working with a notebook on your browser.

### Running the notebook on an AWS GPU instance

1. Go to the [Amazon EC2 Console](https://console.aws.amazon.com/ec2/v2/) and launch an instance.

   * **Choose AMI:** Select a *Deep Learning Ubuntu AMI* from the AWS Marketplace.
   
   * **Choose Instance Type:** Select a GPU compute *p2.xlarge* Instance.
      
   * **Configure Security Group:** Create a custom TCP rule to allow port 8888. This should only be allowed for your public IP. 
   
   * **Add Storage:** (Optional) Increase size to 20 GiB
   
2. SSH to your E2 instance

3. Clone this repository
```
git clone https://github.com/pvt88/neural-creative-transfer-tensorflow.git
```

4. Set up SSL certificates and Jupyter

Firstly, we will need to generate a password for your notebook. Open a python shell and run:
```python
from notebook.auth import passwd
passwd()
Enter password:
Verify password:
```
Once you enter a password, it should display a hash of your password.
```python
Out[2]: 'sha1:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
```
Copy your above password and update the setup.sh script with it: 
```python
c.NotebookApp.keyfile = u'$SSL_CERTIFICATE_DIR/mykey.key'
c.NotebookApp.open_browser = False
c.NotebookApp.password = u'sha1:<your hashed password>'
```
You can now run the setup script to install tensorflow, cuda and the other required packages. It will also configure your SSL certificate and jupyter notebook.
```
bash setup.sh
```

5. Launch the jupyter notebook

... to be continued