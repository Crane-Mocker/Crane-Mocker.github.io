# Does proxy hide my IP?


<!-- vim-markdown-toc GFM -->

* [The story began](#the-story-began)
* [Searching for reasons](#searching-for-reasons)

<!-- vim-markdown-toc -->

## The story began

I was going to find a new job, before logining the website, I checked my IP. I live in China and use vpn. At first I used Baidu and ip138, it showed my real ip. Then I used Google and whatismyipaddress.com, it showed the IP in Korea, the IP of the vps. 

I use v2ray + Chrome + SwitchyOmega, I want to know why ip138 showed my real IP and how can I hide it in daily life. (Ofc, Tor browser is wonderful choice.)

## Searching for reasons

According to the READEME of [SwithyOmega](https://github.com/FelisCatus/SwitchyOmega).

> This project contains a PAC generating module called omega-pac, which handles the profiles model and compile profiles into PAC scripts. This module is standalone and can be published to npm when the documentation is ready.

According to the https://developer.chrome.com/extensions/proxy#bypass_list

> system
> In system mode the proxy configuration is taken from the operating system. This mode allows no further parameters in the ProxyConfig object. Note that the system mode is different from setting no proxy configuration. In the latter case, Chrome falls back to the system settings only if no command-line options influence the proxy configuration.

I use Qv2ray, the defualt setting it bypass the mainland. I banned it and cleaned the cache, still useless. Baidu still showed my real IP. I checked online, "ip138 shows original IP + use vpn", it happens, but nobody told why.
