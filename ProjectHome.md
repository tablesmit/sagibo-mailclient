# Mail Client - A .NET IMAP, POP3 and SMTP for sending email #
> 

&lt;hr&gt;


<b>Author:</b> Sagi bar on

&lt;BR&gt;


<b>Description:</b> It allows sending email messages and add the images in the mail body as "CID:" (Alternate View Linked Resources)

&lt;BR&gt;


<b>License:</b> licensensed under The MIT License (see <a href='http://opensource.org/licenses/mit-license.php'><a href='http://opensource.org/licenses/mit-license.php'>http://opensource.org/licenses/mit-license.php</a></a>
or the license.txt file)

## What's new ? ##
Have a look [MailclientChanges](MailclientChanges.md)!

## Dependencies ##
  * .NET Framework 4.0
  * <a href='http://logging.apache.org/log4net/'>log4net</a> (≥ 2.0.0)- For logs
  * <a href='http://nunit.org/'>NUnit</a> (≥ 2.6.2)- For test

## Features ##
  * Sending Media type as (Html, Plain, Rich text, Xml)
  * Add List of files, To, Cc & Bcc
  * Attached any files
  * Embed images in email
  * Changing the Encoding Type
  * Send Async OR Sync mails

## Install ##
  * Change the App.config OR add the section 'Start email settings' to your project
  * Then change the parameters for your mail account and Run it!

## Usage ##
Set the default "to" in an AppSetting instead and use that from you mail sending logic.

&lt;BR&gt;


Here is the docs for mailSettings: <a href='http://msdn.microsoft.com/en-us/library/w355a94k.aspx'><a href='http://msdn.microsoft.com/en-us/library/w355a94k.aspx'>http://msdn.microsoft.com/en-us/library/w355a94k.aspx</a></a>

General account use:
```
<system.net>
    <mailSettings>
      <smtp from="mail@domain.com">
        <network host="mail.domain.com" port="25" userName="XXX" password="YYY" defaultCredentials="false"/>
      </smtp>
    </mailSettings>
  </system.net>
```

Gmail account use:
```
<system.net>
    <mailSettings>
      <smtp from="yourmail@gmail.com">
        <network host="smtp.gmail.com" port="587" userName="yourmail@gmail.com" password="XXX" enableSsl="true" />
      </smtp>
    </mailSettings>
  </system.net>
```

Network Settings use:
```
<system.net>
    <mailSettings>
      <smtp deliveryMethod="network">
        <network
          host="localhost"
          port="25"
          defaultCredentials="true"
        />
      </smtp>
    </mailSettings>
  </system.net>
```
Open new project and try this examples:

**The First Thing You Must Do**
```
using MailClient;

const string subject = "this is mail subject";
var stringBuilder = new StringBuilder();
stringBuilder.AppendLine("this is a test.");
stringBuilder.AppendLine();

var mailClient = new Mailer
{
    IsAsync = false,
    MessageType = Mailer.MediaType.Html,
    EncodingType = Encoding.UTF8,
};
```

**Example 1 (Send mail To as sync)**:
```
//TODO: Here you need to change the email to in this example there are two email to
const string emailsTo = "one@domain.com,two@domain.com";
var mailAddressTo = new MailAddressCollection();
foreach (var variable in emailsTo.Split(','))
{
    mailAddressTo.Add(variable);
}
mailClient.IsAsync = false;
mailClient.To = mailAddressTo;

mailClient.Send(subject, stringBuilder.ToString());

//TODO: Here is the response, you can use it for your own purpose
if (mailClient.ResponseStatus.Error != null)
{
    //Handle Error :)
    Debug.WriteLine(String.Format(mailClient.ResponseStatus.Error));
}

Debug.WriteLine(mailClient.ResponseStatus.Status);

```

## FUQ - Frequently Unasked Questions ##
<b>Q:</b> What language is MailClient written in?

&lt;BR&gt;


<b>A:</b> MailClient is written in .Net Framework 4.

&lt;BR&gt;




&lt;BR&gt;


<b>Q:</b> I'm on Linux/BSD/Mac/Solaris/Cray/amstrad464/C64/zx81. Can I use MailClient?

&lt;BR&gt;


<b>A:</b> No. (well, maybe if you really, really wanted. But why would you?)

&lt;BR&gt;




&lt;BR&gt;


<b>Q:</b> Is this project really providing value to the world?

&lt;BR&gt;


<b>A:</b> It does to me. And I'm sometimes present in what you call the world.

&lt;BR&gt;




&lt;BR&gt;


<b>Q:</b> How can I help the project?

&lt;BR&gt;


<b>A:</b> Try it out, give feedback/write code and/or spread the word.

&lt;BR&gt;




&lt;BR&gt;


<b>Q:</b> Is MailClient stable?

&lt;BR&gt;


<b>A:</b> No. Currently MailClient is just a newborn. Versioning follows <a href='http://semver.org/'>semantic versioning.</a>

## Acknowledgement ##
MailClient would never have come into existence if I never send bulk of mails.

## Contribute ##
You can help the project in several ways:
  * Report bugs: Take a look at the <a href='http://code.google.com/p/sagibo-mailclient/issues/list'>Issues page</a>. Suggestions and comments are most welcome too.
  * Send patches: If you plan to develop a new module, read the [NewModules](NewModules.md) page.
  * Premium account: Account points or similar to test premium features.
  * Donate: If Plowshare has been useful to you, consider donating using Paypal.
<a href='https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=W4A53QVSR9GMW'>
<img src='https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif' alt='Donate' />
</a>