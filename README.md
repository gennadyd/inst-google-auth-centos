

# How To Set Up Multi-Factor Authentication for SSH & GUI on CentOS
**Install Google-Authenticator**

`sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm`

Once the repository is installed, you can then installed the google-authenticator with the command:

`sudo yum install google-authenticator`
					
**Run the Google-Authenticator wizard**, after which you’ll be provided with a QR code and a Secret Key, Verification Code, and Emergency Scratch codes. Answer with the default to the following questions
 1. Do you want me to update your "~/.google_authenticator" file? **(y/n) y**
 2. Do you want to disallow multiple uses of the same authentication token? This restricts you to one login about every 30s, but it increases your chances 
		to notice or even prevent man-in-the-middle attacks **(y/n) y**
 
 3. By default, tokens are good for 30 seconds. In order to compensate for possible
		time-skew between the client and the server, we allow an extra token before and
		after the current time. If you experience problems with poor time synchronization,
		you can increase the window from its default size of +-1min (window size of 3) to 
		about +-4min (window size of 17 acceptable tokens). Do you want to do so? **(y/n) n**
 4. If the computer that you are logging into isn't hardened against
    brute-force login attempts, you can enable rate-limiting for the authentication module. By default, this limits attackers to no more than 3 login attempts every 30s. Do you want to enable rate-limiting **(y/n) y**

**Scan the bar code or enter it manually into the Google Auth app on your phone.**

<ins>**Choose where you’d like to enable 2 Factor. SSH, Login, and others**</ins>

<ins>*SSH 2 Factor*</ins>

    1.Add "auth required pam_google_authenticator.so" to the end of /etc/pam.d/sshd file.
    2.Change "ChallengeResponseAuthentication no" to "ChallengeResponseAuthentication yes" 
        in the /etc/ssh/sshd_config file.
    3.Restart ssh: sudo systemctl restart sshd
<ins> *Gnome Login 2 Factor*</ins>

Add "auth required pam_google_authenticator.so nullok" to the end of /etc/pam.d/gdm-password file

<ins>*Direct Login Screen*</ins>

Add "auth required pam_google_authenticator.so nullok" to the end of /etc/pam.d/loginfile
