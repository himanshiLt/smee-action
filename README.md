<h3 align="center">Smee Action</h3>
<p align="center">Use <a href="https://smee.io">smee.io</a> to debug Action runs<p>

## Usage

```workflow
workflow "Smee!" {
  on = "push"
  resolves = ["test"]
}

# Place this Action early in your workflow
action "smee" {
  uses = "JasonEtco/smee-action@master"
}

action "test" {
  needs = ["smee"]
}
```

:warning: Heads up! This is only to be used for debugging, not for sensitive data. Smee.io is not secured by any authentication, so anyone with the channel ID can view your payloads as they come in. :warning:

## Seeing the payloads

A common misconception about Smee.io is that the payloads will be available all the time - to see a new payload as its sent, **you must have a browser tab open to the channel URL.** The payloads are stored in `localStorage` in your browser.

## Specifying the channel

By default, this Action will post event payloads to the **smee.io/REPOSITORY_ID** - if you aren't sure what that is, it'll log it for you the first time your run the Action.

You can specify what channel you want to send to:

```workflow
# Using arguments
action "smee" {
  uses = "JasonEtco/smee-action@master"
  args = "--channel my-channel"
}

# Using a secret
action "smee" {
  uses = "JasonEtco/smee-action@master"
  secrets = ["SMEE_CHANNEL"]
}
```