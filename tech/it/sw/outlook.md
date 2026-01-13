# Overview

# Rules

- Differences between server-side rules and client-side rules
    + https://support.microsoft.com/en-us/office/edit-or-fix-a-broken-rule-in-outlook-e1847992-8aa1-4158-8e24-ad043decf1eb#bkmk_servervclient
    + Server-side rules:
        * It use conditions and actions handled by the Exchange server,
          and these rules run whether or not you log in to Outlook on
          your computer.
        * Here’s an example of a server-side rule:
            - `From <people or distribution list in the GAL or your contacts list>, move it to the <specified> folder`
            - This rule uses all Exchange server information, like
              moving a message from a sender who’s in a Global Address
              List to a specific folder that’s in your Exchange mailbox.
        * Server-side rules can move mail to a specified folder, for
          example, when that folder also exists on the server.
        * A server-side rule cannot move mail to a folder that only
          exists on your device.
    + Client-side rules:
        * Client-side rules have at least one condition or action that
          uses an Outlook feature, and `they don’t run until you log into
          classic Outlook` for Windows with the account that you used to
          create the rule.
        * For example, this is a client-only rule:
            - `From <people or distribution list>, flag message to <play a sound>`
        * In this example, you ask the rule to play a sound when you
          receive a message, and this condition can be performed only by
          Outlook, which makes it a client-only rule.
- Outlook rules run from top to bottom in the order they appear in the
  "Rules" list.
    + Crucially, rules with a "stop processing" action will halt further
      rule checks for that email.
