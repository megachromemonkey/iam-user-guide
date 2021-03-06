# Enabling a Hardware MFA Device \(Console\)<a name="id_credentials_mfa_enable_physical"></a>

A hardware MFA device generates a six\-digit numeric code based upon a time\-synchronized one\-time password algorithm\. The user must type a valid code from the device when prompted during the sign\-in process\. Each MFA device assigned to a user must be unique; a user cannot type a code from another user's device to be authenticated\. 

Hardware MFA devices and [U2F security keys](id_credentials_mfa_enable_u2f.md) are both physical devices that you purchase\. The difference is that hardware MFA devices generate a code that you view and then enter when prompted when signing it to AWS\. With a U2F security key, you don't see or type an authentication code\. Instead, the U2F security key generates a response without presenting it to the user and the service validates it\. For specifications and purchase information for both device types, see [Multi\-Factor Authentication](http://aws.amazon.com/iam/details/mfa/)\.

You can enable a hardware MFA device for an IAM user from the AWS Management Console, the command line, or the IAM API\. To enable an MFA device for your AWS account root user, see [Enable a Hardware MFA Device for the AWS Account Root User \(Console\)](#enable-hw-mfa-for-root)\.

You can enable **one** MFA device \(of any kind\) per root user or IAM user\.

**Note**  
If you want to enable the device from the command line, use [https://docs.aws.amazon.com/IAM/latest/CLIReference/userenablemfadevice.html](https://docs.aws.amazon.com/IAM/latest/CLIReference/userenablemfadevice.html) [aws iam enable\-mfa\-device](https://docs.aws.amazon.com/cli/latest/reference/iam/enable-mfa-device.html)\. To enable the MFA device with the IAM API, use the [https://docs.aws.amazon.com/IAM/latest/APIReference/API_EnableMFADevice.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_EnableMFADevice.html) action\. 

**Topics**
+ [Enable a Hardware MFA Device for an IAM User \(Console\)](#enable-hw-mfa-for-iam-user)
+ [Enable a Hardware MFA Device for the AWS Account Root User \(Console\)](#enable-hw-mfa-for-root)
+ [Replace or "Rotate" a Physical MFA Device](#replace-phys-mfa)

## Enable a Hardware MFA Device for an IAM User \(Console\)<a name="enable-hw-mfa-for-iam-user"></a>

 You can enable a hardware MFA device from the AWS Management Console\.

**To enable a hardware MFA device for an IAM user \(console\)**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Users**\.

1. Choose the name of the user for whom you want to enable MFA, and then choose the **Security Credentials** tab\.

1. Next to **Assigned MFA device**, choose **Manage**\.

1. In the **Manage MFA Device** wizard, choose **Hardware MFA device** and then choose **Continue**\.

1. Type the device serial number\. The serial number is usually on the back of the device\.

1. In the **MFA Code 1** box, type the six\-digit number displayed by the MFA device\. You might need to press the button on the front of the device to display the number\.  
![\[IAM Dashboard, MFA Device\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/MFADevice.png)

1. Wait 30 seconds while the device refreshes the code, and then type the next six\-digit number into the **MFA Code 2** box\. You might need to press the button on the front of the device again to display the second number\.

1. Choose **Assign MFA**\.
**Important**  
Submit your request immediately after generating the authentication codes\. If you generate the codes and then wait too long to submit the request, the MFA device successfully associates with the user but the MFA device becomes out of sync\. This happens because time\-based one\-time passwords \(TOTP\) expire after a short period of time\. If this happens, you can [resync the device](id_credentials_mfa_sync.md)\.

The device is ready for use with AWS\. For information about using MFA with the AWS Management Console, see [Using MFA Devices With Your IAM Sign\-in Page](console_sign-in-mfa.md)\.

## Enable a Hardware MFA Device for the AWS Account Root User \(Console\)<a name="enable-hw-mfa-for-root"></a>

You can use IAM in the AWS Management Console to configure and enable a hardware MFA device for your root user\. To enable MFA devices for the AWS account, you must be signed in to AWS using your root user credentials\. You cannot enable an MFA device for the AWS account root user with the AWS CLI, AWS API, Tools for Windows PowerShell, or any other command\-line tool\.

If your MFA device is lost, stolen, or not working, you can still sign in using alternative factors of authentication\. If you can't sign in with your MFA device, you can sign in by verifying your identity using the email and phone that are registered with your account\. Before you enable MFA for your root user, review your account settings and contact information to make sure that you have access to the email and phone number\. To learn about signing in using alternative factors of authentication, see [What If an MFA Device Is Lost or Stops Working?](id_credentials_mfa_lost-or-broken.md)\. To disable this feature, contact [AWS Support](https://console.aws.amazon.com/support/home#/)\.

**Note**  
If you are using an AWS account created after September 14, 2017, you might see differences in the following console pages: **Sign in using MFA** and **Troubleshoot your authentication device**\. However, the same features are provided\. In either case, if you cannot verify your account email address and phone number using alternative factors of authentication, contact [AWS Support](https://aws.amazon.com/forms/aws-mfa-support) to deactivate your MFA setting\.<a name="enable_physical_root"></a>

**To enable the MFA device for your root user \(console\)**

1. Sign in to the AWS Management Console\.
**Important**  
To manage MFA devices for the AWS account, you must use your root user credentials to sign in to AWS\. You cannot manage MFA devices for the root user while signed in with other credentials\.

1. Do one of the following:
   + **Option 1**: Choose **Dashboard**, and under **Security Status**, expand **Activate MFA on your root account**\. 
   + **Option 2**: On the right side of the navigation bar, choose on your account name, and then choose **My Security Credentials**\. If necessary, choose **Continue to Security Credentials**\. Then expand the **Multi\-Factor Authentication \(MFA\)** section on the page\.  
![\[My Security Credentials in the navigation menu\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/security-credentials-root.shared.console.png)

1. Choose **Manage MFA** or **Activate MFA**, depending on which option you chose in the preceding step\.

1. In the wizard, choose **Hardware MFA device** and then choose **Continue**\.

1. In the **Serial Number** box, type the serial number that is found on the back of the MFA device\.

1. In the **MFA Code 1** box, type the six\-digit number displayed by the MFA device\. You might need to press the button on the front of the device to display the number\.  
![\[IAM Dashboard, MFA Device\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/MFADevice.png)

1. Wait 30 seconds while the device refreshes the code, and then type the next six\-digit number into the **MFA Code 2** box\. You might need to press the button on the front of the device again to display the second number\.

1. Choose **Assign MFA**\. The MFA device is now associated with the AWS account\.
**Important**  
Submit your request immediately after generating the authentication codes\. If you generate the codes and then wait too long to submit the request, the MFA device successfully associates with the user but the MFA device becomes out of sync\. This happens because time\-based one\-time passwords \(TOTP\) expire after a short period of time\. If this happens, you can [resync the device](id_credentials_mfa_sync.md)\.

   The next time you use your root user credentials to sign in, you must type a code from the MFA device\.

## Replace or "Rotate" a Physical MFA Device<a name="replace-phys-mfa"></a>

You can have only one MFA device assigned to a user at a time\. If the user loses a device or needs to replace it for any reason, you must first deactivate the old device\. Then you can add the new device for the user\.
+ To deactivate the device currently associated with a user, see [Deactivating MFA Devices](id_credentials_mfa_disable.md)\.
+ To add a replacement hardware MFA device for an IAM user, follow the steps in the procedure [Enable a Hardware MFA Device for an IAM User \(Console\)](#enable-hw-mfa-for-iam-user) earlier in this topic\.
+ To add a replacement virtual MFA device for the AWS account root user, follow the steps in the procedure [Enable a Hardware MFA Device for the AWS Account Root User \(Console\)](#enable-hw-mfa-for-root) earlier in this topic\.