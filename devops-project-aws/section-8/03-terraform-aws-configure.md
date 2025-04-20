# Connect Terraform with AWS to Create AWS Resources

## 1. **Install AWS CLI**
### On Linux:
- Download and install AWS CLI:
  ```sh
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  unzip awscliv2.zip
  sudo ./aws/install
  ```
- Verify installation:
  ```sh
  aws --version
  ```

### On Windows:
- Download the installer from [AWS CLI Official Site](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- Run the installer and follow the setup instructions.
- Verify installation:
  ```sh
  aws --version
  ```

### On macOS:
- Install using Homebrew:
  ```sh
  brew install awscli
  ```
- Verify installation:
  ```sh
  aws --version
  ```

## 2. **Configure AWS CLI**
- Run the following command to configure AWS credentials:
  ```sh
  aws configure
  ```
- Provide the following details when prompted:
  - AWS Access Key ID
  - AWS Secret Access Key
  - Default region name (e.g., `us-east-1`)
  - Default output format (e.g., `json` or `text`)

**NOTE**: Above command stores AWS credentials in `~/.aws/credentials`, Terraform uses those credentails to interact with AWS.