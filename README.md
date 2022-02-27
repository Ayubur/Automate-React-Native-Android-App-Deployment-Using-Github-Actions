To automate the deployment , it requires the use of [Github Actions]([https://docs.github.com/en/actions/security-guides/encrypted-secrets]). We Will be needing to use them because:
- We will need to sign our application
- We are going to give this action permission to submit our built application to the Google Play Store


We can create Github Secrets by going  **Our repository -> Settings -> Secrets -> New repository secret** . We need to create secrets for :
- The Signing Key (secrets.SIGN_KEY)
- The Key Alias (secrets.ALIAS)
- The Store Key Password (secrets.STORE_KEY_PASSWORD)
- The Key Password (secrets.KEY_PASSWORD)


Once we have signed the .aab file we can deploy it to the Google Play Store. Now we need to allow this GitHub Action the permission to deploy applications for us on Google Play. We use a [Service Account](https://cloud.google.com/compute/docs/access/service-accounts) .

#### Creating a Service Account
To create a service account, we need to log in our Google Cloud Console Account. Then, on the main page , in the left hand side menu, there will be a list item titled Service Accounts. We need to go to **Service Accounts -> Create Service Account** . In the window that opens, you will have to enter in the service’s name and you can also enter a description. The name given here will be the unique identifier of this service account.

- In the second step we will be asked to give this service account a role. From the **Select A Role** dropdown, choose **Basic → Editor**.
- Finally, in the third step, need to fill out our email in both places under the "Grant users access to this service account" section.

After pressing the done button, we will need to create a key for this service account. The action will use this key to be identified by Google Play.

To create the key, click the three horizontal dots under the Actions label in the main service account screen. In the menu that appears, select **Manage keys**. 

- In this window, we will create a key by selecting the New Key button and choosing "Create new key" from the menu that appears.
- Now we have the option of choosing the format of our new key – the default is JSON and we will leave it selected. Click create.

Once we have done so, a file will be downloaded to your computer. Make sure to keep this file as it has all the data relevant for our service account and we won’t be able to download it again. Now, we need to make Google Play aware of this service account.

#### Set up Google Play Console
We need to go our Google Play Console and head over to **Setup -> API Access**.
- If we scroll down the page, we will see a section titled Service Accounts. we should be able to see the service account we created previously. Click the Grant Access link.
- In the settings that open, head over to App permissions. Here we will choose which application this service account interacts with.
- Under Account permissions, everything under the releases section should be checked.
- Once we are done, need to the Invite user button located in the bottom right corner.