# Tree Guardian

Track the changes into the filesystem and trigger callback on changes 
 detecting.


## Getting Started

### Installation

```bash
pip install tree-guardian
```

### Usage (Python)

Observe the changes into your project.
```python
from tree_guardian import observe

# Target function to trigger
def cb():
    from time import time

    print('[{}] Changes detected...'.format(time()))

observe(cb)  # Run observer
```

Run in background.
```python
from time import sleep
from threading import Event
from tree_guardian import observe


# Target function to trigger
def cb():
    from time import time

    print('[{}] Changes detected...'.format(time()))


event = Event()
observe(cb, run_async=True, event=event)  # Run observer

# Type your code below...

try:
    sleep(10)  # Run for 10 seconds or until interrupted
except KeyboardInterrupt:
    event.set()
```

### Usage (Cli)

You can also use tree-guardian commands in shell. To make observe, run, for example:
```shell
tree-guardian-observe --command='[YOUR SHELL COMMAND HERE]'
```

This command supports the following params:
```shell
usage: tree-guardian-observe [-h] [-d] -c CALLBACK [-p PATH] [-e [EXCLUDE ...]]

Observe directory and trigger callback on change detection

optional arguments:
  -h, --help            show this help message and exit
  -d, --debug           run observe on debug mode; it also displays all trigger-command output
  -c [CALLBACK_COMMAND ...], --cmd [CALLBACK_COMMAND ...], --command [CALLBACK_COMMAND ...], --callback [CALLBACK_COMMAND ...], --callback-command [CALLBACK_COMMAND ...]
                        trigger command
  -p PATH, --path PATH  the observable root path
  -e [EXCLUDE ...], --exclude [EXCLUDE ...]
                        excluded files from observe

```

Call it with `--help` flag to get more details.
```shell
tree-guardian-observe --help
```
