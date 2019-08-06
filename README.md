## Mesibo Real-Time API
Mesibo offers everything to make your app real-time and scalable for your first billion users and the next. It's modular, lightweight and easy to integrate.

Mesibo supports almost all popular platforms and languages for you to quickly build your applications. Whether you are developing mobile apps (Android, iOS, Java, Objective-C, C++), web apps (Javascript), integrating with backend (Linux, MacOS, Windows, Python, C++) or creating cool devices using Raspberry PI, mesibo has APIs for you.

Mesibo's high performance C++ and Python libraries enable you to interface your chat clients with various scientific computing and machine learning systems on your backend like TensorFlow, Matlab, Octave, NumPy etc to create a powerful chat experience.

This repo contains the source code for Mesibo Python API.

- **Website:** https://mesibo.com
- **Documentation:** https://mesibo.com/documentation/


## Prerequisites
Building Mesbio Python modules requires the following software installed:

**1. Mesibo C/C++ library**

Install the shared library by following the instructions [here](https://mesibo.com/documentation/install/linux/#install-using-the-convenience-script)

**2.Python 3(3.4.x or newer preferred) / Python 2 (2.7.x or newer preferred)**

On CentOS,Debian and derivatives (Ubuntu): python, python-dev (or python3-dev/python2-dev)

Make sure that the Python package distutils is installed before continuing. For example, in Debian GNU/Linux, installing python-dev also installs distutils.

**3.Compiler**

 C/C++ compiler.GCC 4.x (and later)are recommended. 
 
```
|-- include
|-- setup.py
|-- src
|-- tests

```

## Basic Installation

To build and install mesibo python module 
```
sudo python setup.py install

```


To perform an in-place build that can be run from the source folder run:
```
python setup.py build_ext --inplace
```

## API Usage
```python
import mesibo
from mesiboNotify.mesiboNotify import mesiboNotify

#Mesibo invokes various Listeners for various events.
#For example, when you receive a message, receive an incoming call etc
#mesiboNotify is a class of listeners that can be invoked to get real-time notification of events  


class test_mesiboNotify(mesiboNotify):

    def __init__(self):
        pass

    def on_status(self, status, sub_status, channel, p_from):
        print("===>on_status: " + str(status) + " substatus: " +
              str(sub_status) + " channel:" + str(channel) + "from: " + str(p_from))
        
        if(int(status) == 1 ): #Connection is setup and you are online
            msg_params = {"id":mesibo.random()}
            to = "917019882153" #Destination user ID
            data = "Hello from mesibo"
            datalen = len(data)
            mesibo.send_message(msg_params,to,data,datalen)


        return 1
        

    def on_message(self, message_params_dict, p_from, data, p_len):
        #invoked on receiving a new message or reading database messages 
        print("===>on_message: from " + str(p_from) + " of len " + str(p_len))
        print(data[:p_len])  # data buffer/Python bytes object
        print(str(data[:p_len], encoding='utf-8', errors='strict'))

        print("with message parmeters:")
        print(message_params_dict)

        return 1

    def on_messagestatus(self,  message_params_dict, p_from, last):
        #Invoked when the status of outgoing or sent message is changed
        print("===>on_messagestatus: from " +
              str(p_from) + " " + str(last))
        print("with message_parameters")
        print(message_params_dict)
        return 1


#get your accesstoken for the appname you registered from https://mesibo.com/console
mesibo.set_accesstoken("your_access_token")
mesibo.set_database("mesibo.db")
mesibo.set_notify(test_mesiboNotify)
mesibo.set_device(1, "your_device_id", "your_app_name", "1.0.0")
mesibo.start()
mesibo.wait()
```
