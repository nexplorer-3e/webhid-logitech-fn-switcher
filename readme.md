# WebHID Logitech Keyboard Fn Enabler

This is a simple demo using WebHID to switch Logi keyboards' Fn-key as default (or not).

As of 2025 there are only chromium-based browsers that supports WebHID.
So chromium is a dependency.


## todo

- [ ] deploy to cloudflare
- [ ] ios reimplement
- [ ] (w/ localstorage) make the input box presist when you need to open the page again
- [ ] allow user to submit their device info & payload
- [ ] figure out the real meaning of the payload (need to seek for hidpp docs)
- [ ] modern frontend (might be impossible as this is just proof-of-concept)

## acknow

k380 payload from https://github.com/jergusg/k380-function-keys-conf

k480 payload from https://github.com/embuc/k480_conf

k81{0,1} payload from https://github.com/keighrim/k810fn

origin idea from https://www.trial-n-error.net/posts/2012/12/31/logitech-k810-keyboard-configurator/

code skeleton by gemini-2.5-pro (it messed up the payload, let me debug for 4hrs though),
responsive support by grok-code-fast-1.
qwen3 indicates the payload may be proprietary format.

## License

except the payloads from above, the code is licensed under AGPL-3.0.

## caveat of Linux hidraw to webhid

this has been mentioned in the html. Still i want to reminder for those
want to try hidraw with know little about io like me:

put the first byte of hidraw payload to the first arg of `device.sendReport`,
as sendReport need an descriptor to send.

## relation with hidpp

This is just a small project created on a whim.
Therefore, the actual meaning of the payload in the means of Logitech HID++ is still unclear.

Check https://github.com/cvuchener/hidpp if u are interested.

Known information:

- the fn controller has the following traits:
  - outputDescriptor = 0x10
  - usagePage = 0xff00
- in hidraw format, the control bit is always on the 5th byte,
0x0 is default fn keys, and 0x1 is not (mode key (?) default).
