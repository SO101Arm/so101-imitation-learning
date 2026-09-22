# 5. Hugging Face

## Hugging Face Platform

### What is Hugging Face?

- **Hugging Face** is an open‑source platform for sharing and managing machine learning models, datasets, and applications.
- It provides popular ML libraries such as **Transformers** and **Diffusers**, along with the **Hugging Face Hub**.
- The Hub serves as a central repository for sharing and downloading models and datasets, including datasets used in LeRobot.

## Hugging Face Login

### How to create a Hugging Face account

- Go to <https://huggingface.co/login?next=%2Fsettings%2Ftokens> and click **Sign Up**.
- Enter your email, password, and username to create an account.
- Verify your email and log in to your account.
- Your username will be used in your Hub repository path, e.g. `username/dataset-name`.

## Create Hugging Face Access Tokens

### About access tokens

- **Access Token:** a unique key used to authenticate with the Hugging Face Hub instead of a password, allowing secure authentication through the CLI or API.
- **Token types:**
  - **Fine‑grained** — specific permissions.
  - **Read** — read‑only access.
  - **Write** — both reading and writing.
- A **Write** token is required to upload models or datasets to the Hugging Face Hub.

### Creating an access token

- On the **Access Tokens** page, click **+ Create new token** in the top‑right corner.
- If no token exists, "You have no Access Token" will be displayed.
- Multiple tokens can be created and managed separately for different purposes.
- Select **Write** as the token type if you need to upload models or datasets — **the permission cannot be changed after creation**.
- Use a descriptive token name, such as `IL` or `lerobot-upload`, to identify its purpose.
- The token is displayed **only once** after creation, so copy and store it securely.
- If the token is lost, you must create a new token.

### Saving the access token

- After creating the token, click **Copy** in the modal window to save it.
- The token cannot be viewed again after closing the modal.
- The token starts with `hf_`, and the modal displays the token name and permissions (Write) for confirmation.

## Add your Access Token to the CLI

```bash
hf auth login --token ${HUGGINGFACE_TOKEN} --add-to-git-credential
```

### Verify Hugging Face Authentication

```bash
hf auth whoami
```

### Why add the token to the CLI?

- The Access Token allows the Hugging Face CLI to authenticate your account.
- It enables LeRobot to upload and download datasets or models from the Hugging Face Hub.
- Once authenticated, you do not need to enter the token every time you use Hugging Face commands.

## Configure Git credential storage

```bash
git config --global credential.helper store
```

## Set Hugging Face username

```bash
HF_USER=${YOUR_HF_NAME}
```

## Verify Hugging Face username

```bash
echo $HF_USER
```

---

Previous: [← 4. Teleoperation](04-teleoperation.md) · Next: [6. Problem Definition →](06-problem-definition.md)
