# Uploading Images to AWS S3 Bucket From NextJS

This is assuming you have a AWS account created

## Creating A New AWS Bucket

### Create a new [IAM User](https://aws.amazon.com/iam/)

```
An AWS Identity and Access Management (IAM) user is an entity that represents the human user/workload who can access and interact with AWS. These users usually require name and credentials.
```

Go to the Users tab, select **Add users**.

Add a name for the new user, select **Attach existing policies directly**, and then add **AmazonS3FullAccess** to the list.

After that continue and finish creating the user.

Navigate to the user's details by clicking on the user's name and head to the **Security credentials** tab.

Locate **Access keys** and from there press **create access key** which will provide you with a key and secret that you should note down.

### Installing [AWS CLI](https://docs.aws.amazon.com/cli/v1/userguide/install-macos.html)

Python 3.6+ is required to install and defaulted and can be done by installing the latest version of [python](https://www.python.org/downloads/) and running `ln -s -f /usr/local/bin/python3.* /usr/local/bin/python` in the command line where the `*` will be the installed python version.

- This method is for MacOS

I installed it via `pip3 install awscli`.

Type `aws --version` to verify that aws is installed on your machine.

- If it is giving you command not found error, check that the PATH to your python folder where awscli is installed in is correct in your shell's profile script. For me it was in `.zshrc`.

### Configuring AWS

Run `aws configure` and enter your access key ID and secret along with the default region name.

Create a `.env.local` in your NextJS project and input your access key ID and secret.

### Setting Up CORS

```
Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain.
```

Go to your bucket and head to the **Permissions** tab. From there locate the **Cross-origin resource sharing (CORS)** section and add

```
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "PUT",
            "POST",
            "GET"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]
```

to the configuration. This rule allows all header requests in a preflight options request through `Access-Control-Request-Headers` header. This rule also allow PUT, POST, and GET requests from all origins.
