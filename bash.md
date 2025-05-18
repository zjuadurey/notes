# vpn

## test the ip
``
curl cip.cc
``

## settings for ssr-command-client

alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080"
alias unsetproxy="unset ALL_PROXY"
alias ip="curl http://ip-api.com/json/?lang=zh-CN"

## auto open ssr-command-client
unsetproxy
/usr/local/bin/shadowsocksr-cli -S
setproxy
/usr/local/bin/shadowsocksr-cli -s 1

## reset bash
source ~/.bashrc