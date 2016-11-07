## Redmine omniauth gitlab

This plugin is used to authenticate Redmine users using gitlab's OAuth2 provider.

The major logic as similar as [redmine_omniauth_google](https://github.com/twinslash/redmine_omniauth_google)

### Installation:

Download the plugin and install required gems:

```console
cd /path/to/redmine/plugins
git clone https://github.com/applewu/redmine_omniauth_gitlab
cd /path/to/redmine
bundle install
```

Restart the redmine
```console
/path/to/redmine/ctlscript.sh restart
```

### Registration

To authenticate via gitlab you must first register your redmine instance via your gitlab

* Go to your profile setting area.
* Click "Applications"
* Type a "Name" for the application, e.g. "My Redmine"
* Enter "https://mydomain.com/redmine/oauth2callback" as "Redirect URI", where "mydomain.com/redmine" is the domain / path for your redmine instance. *** The plugin will not work without this setting ***
* Click "Save application"
* Save the "Application ID" and "Secret" for the configuration of the Redmine plugin (see below)

### Configuration

* Login as a user with administrative privileges. 
* In top menu select "Administration".
* Click "Plugins"
* In plugins list, click "Configure" in the row for "Redmine Omniauth gitlab plugin"
* Enter "Application ID"  & "Secret" shown when you registered your application via gitlab as Сlient ID & Client Secret.
* Check the box near "Oauth authentication"
* Click Apply. 
 
Users can now to use their gitlab Account to log in to your instance of Redmine.

Additionaly
* Setup value Autologin in Settings on tab Authentification

### Other options

By default, all user email domains are allowed to authenticate through gitlab.
If you want to limit the user email domains allowed to use the plugin, list one per line in the  "Allowed domains" text box.

For example:

```text
onedomain.com
otherdomain.com
```

With the above configuration, only users with email addresses on the domains "onedomain.com" and "otherdomain.com" will be allowed to acccess your Redmine instance using gitlab OAuth.

### Authentication Workflow

1. An unauthenticated user requests the URL to your Redmine instance.
2. User clicks the "Login via gitlab" buton.
3. The plugin redirects them to a gitlab sign in page if they are not already signed in to their gitlab account.
4. gitlab redirects user back to Redmine, where the gitlab OAuth plugin's controller takes over.

One of the following cases will occur:
1. If self-registration is enabled (Under Administration > Settings > Authentication), user is redirected to 'my/page'
2. Otherwse, the an account is created for the user (referencing their gitlab OAuth2 ID). A Redmine administrator must activate the account for it to work.
