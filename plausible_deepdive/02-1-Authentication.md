# Authentication

The main authentication is being handled by the AuthController.
It handles the registration of users. With some standard credientials

Name, email, password and password confirmation.

They can also register by referrals known as invitations.

After successfully registering an account and logging in, they will be required to enter an activation code that was sent to their email.

They have an additional validation where the user is limited to 5 attempts per minute when logging in.
## TODO: Need to check how they limit password attempts per minute.

Their auth controller also contains some extra routes such as settings, `/me` and password reset.
