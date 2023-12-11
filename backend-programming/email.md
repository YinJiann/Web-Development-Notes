# Email

## NodeMailer

```
npm i nodemailer
```

```javascript
const nodemailer = require('nodemailer');

const sendEmail = async options => {
  // 1) Create a transporter. E.g. GMAIL
  const transporter = nodemailer.createTransport({
    //service: "Gmail"
    host: process.env.EMAIL_HOST,
    port: process.env.EMAIL_PORT,
    auth: {
      user: process.env.EMAIL_USERNAME,
      pass: process.env.EMAIL_PASSWORD
    }
  });

  // 2) Define the email options
  const mailOptions = {
    from: 'Jonas Schmedtmann <hello@jonas.io>',
    to: options.email,
    subject: options.subject,
    text: options.message
    // html:
  };

  // 3) Actually send the email
  await transporter.sendMail(mailOptions);
};

module.exports = sendEmail;
```



## Mailtrap

* Used for development
* Send real email, but instead to destination, to mailtrap
* PostMan for email
