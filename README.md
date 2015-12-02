# csfind

Find CloudStack resource ID

## Installation

1. Install [cs](https://github.com/exoscale/cs) 
2. Create `~/.cloudstack.ini` for your CloudStack environment
3. Install [fzf](https://github.com/junegunn/fzf)
4. Install `csfind`
  
  Download `csfind` script and put it within your `PATH` as below.

  `curl -s -o /usr/local/bin/csfind https://raw.githubusercontent.com/atsaki/csfind/master/csfind && chmod +x /usr/local/bin/csfind`

## Usage

`csfind` fetches CloudStack resource information using API and open `fzf` window.
You can select some item using powerful `fzf` interface and get their IDs.

```bash
csfind template
```

## Example

### Deploy virtual machine

```bash
cs deployVirtualMachine name=$(read -e -p "name: " && echo $REPLY) \
                        zoneid=$(csfind zone) \
                        templateid=$(csfind template CentOS) \
                        serviceofferingid=$(csfind serviceoffering)
```

### Destroy virtual machine

You can select multiple items and delete or update them at once. 

```bash
csfind vm | xargs -I {} cs destroyVirtualMachine expunge=true id={}
```
## License

MIT

## Authour

Atsushi Sasaki (@atsaki)
