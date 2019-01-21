# Filesystem Transport Bundle for Symfony Messenger

[![Latest Stable Version](https://poser.pugx.org/pnz/messenger-filesystem-transport-bundle/version)](https://packagist.org/packages/pnz/messenger-filesystem-transport-bundle)
[![Total Downloads](https://poser.pugx.org/pnz/messenger-filesystem-transport-bundle/downloads)](https://packagist.org/packages/pnz/messenger-filesystem-transport-bundle)
[![Latest Unstable Version](https://poser.pugx.org/pnz/messenger-filesystem-transport-bundle/v/unstable)](//packagist.org/packages/pnz/messenger-filesystem-transport-bundle)
[![License](https://poser.pugx.org/pnz/messenger-filesystem-transport-bundle/license)](https://packagist.org/packages/pnz/messenger-filesystem-transport-bundle)

Integrates the [Filesystem Transport](https://packagist.org/packages/pnz/messenger-filesystem-transport) to Symfony.

## Install

```bash
composer require pnz/messenger-filesystem-transport-bundle
```

This transport handles the `filesystem://` schema, use the `FilesystemTransportFactory`
to create the transport.
Symfony configuration:

Configure the Filesystem transport:
```yaml
#  config/packages/messenger.yaml
parameters:
  # Default ENV value: the queue messages will be stored in the `var/queue` folder,
  # The trailing `//` is required for match the `filesystem://` schema
  env(MESSENGER_TRANSPORT_DSN): "filesystem://%kernel.project_dir%/var/queue"

framework:
    messenger:
        transports:
            filesystem: '%env(resolve:MESSENGER_TRANSPORT_DSN)%'

        routing:
            App\Message\MyMessage: filesystem
```

## Configuration

Check the [Filesystem Transport](https://packagist.org/packages/pnz/messenger-filesystem-transport) documentation.

In short, the DSN includes the following query parameters:

- `compress`: Enable/Disable compression of messages storage (gzinflate/gzdeflate), use `compress=true` (default: false)
- `loop_sleep`: Define the sleep interval between loops in micro-seconds, use `loop_sleep=MICRO-SECONDS` (default: 500000)

Example:
```bash
# .env

# Enable compression, and sleep for 0.8 seconds during loops if the queue is empty
MESSENGER_TRANSPORT_DSN="filesystem://%kernel.project_dir%/var/queue/default?compress=true&loop_sleep=800000"
```
