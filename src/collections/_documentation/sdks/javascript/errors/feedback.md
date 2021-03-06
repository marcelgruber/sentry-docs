---
title: Add User Feedback
excerpt: ""
---
When a user experiences an error, Sentry provides the ability to collect additional feedback. This type of feedback is useful when you may typically render a plain error page (the classic 500.html). 

To collect feedback, use the embeddable JavaScript widget, which requests and collects the user's name, email address, and a description of what occurred. When feedback is provided, Sentry pairs the feedback with the original event, giving you additional insights into issues.

The screenshot below provides an example of the User Feedback widget, though yours may differ depending on your customization:

[{% asset user_feedback_widget.png alt="An example of a user feedback widget with text boxes for user name, email, and additional details about the break." %}]({% asset user_feedback_widget.png @path %})

### Integrate the Feedback Widget

To integrate the widget, you'll need to be running our JavaScript SDK (2.1 or newer). The widget authenticates with your public DSN, then passes in the client-side generated Event ID. 

**Note:** If you'd prefer an alternative to the widget, you can use the User Feedback API.

If you're using a framework such as React or Angular, we recommend collecting user feedback in your error-handling component. Examples are provided in the platform-specific documentation.

If you're not using a framework, you can collect feedback just before an event is sent using `beforeSend`:

```js
<script src="https://browser.sentry-cdn.com/5.15.5/bundle.min.js" integrity="sha384-wF7Jc4ZlWVxe/L8Ji3hOIBeTgo/HwFuaeEfjGmS3EXAG7Y+7Kjjr91gJpJtr+PAT" crossorigin="anonymous"></script>

<script>
  Sentry.init({
    dsn: '___Public_DSN___',
    beforeSend(event, hint) {
      // Check if it is an exception, and if so, show the report dialog
      if (event.exception) {
        Sentry.showReportDialog({ eventId: event.event_id });
      }
      return event;
    }
  });
</script>
```

### Modify the Widget

You can customize the widget to your team's needs, especially for localization purposes. All options can be passed through the `showReportDialog` call.

| Parameter | Default |
| ------------- | --- |
| `eventId` | Manually set the id of the event. |
| `dsn` | Manually set dsn to report to. |
| `user` | Manually set user data _[an object with keys listed above]_. |
| `user.email` | User's email address. |
| `user.name` | User's name. |
| `lang` | _[automatic]_ – **override for Sentry’s language code** |
| `title` | It looks like we’re having issues. |
| `subtitle` | Our team has been notified. |
| `subtitle2` | If you’d like to help, tell us what happened below. – **not visible on small screen resolutions** |
| `labelName` | Name |
| `labelEmail` | Email |
| `labelComments` | What happened? |
| `labelClose` | Close |
| `labelSubmit` | Submit |
| `errorGeneric` | An unknown error occurred while submitting your report. Please try again. |
| `errorFormEntry` | Some fields were invalid. Please correct the errors and try again. |
| `successMessage` | Your feedback has been sent. Thank you! |
| `onLoad` | n/a |

