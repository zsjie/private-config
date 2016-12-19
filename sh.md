# shell 配置

proxy：
```shell
# proxy
YBB=http://127.0.0.1:9743

# default proxy
defp=$YBB

# command noproxy
function noproxy
{
    unset http_proxy HTTP_PROXY https_proxy HTTPS_PROXY all_proxy ALL_PROXY ftp_proxy FTP_PROXY dns_proxy DNS_PROXY JAVA_OPTS GRADLE_OPTS MAVEN_OPTS
    echo "clear proxy done"
}

function setproxy
{
    #parse arg
    arrIN=(${1/:/ })
    # no args, use default
    if [[ ${#arrIN[*]} -eq 0 ]]; then
        http_proxy=$defp
        HTTP_PROXY=$defp
    fi
    all_proxy=$http_proxy
    ALL_PROXY=$http_proxy
    ftp_proxy=$http_proxy
    FTP_PROXY=$http_proxy
    dns_proxy=$http_proxy
    DNS_PROXY=$http_proxy
    https_proxy=$http_proxy
    HTTPS_PROXY=$https_proxy
    JAVA_OPTS="-Dhttp.proxyHost=$HOST -Dhttp.proxyPort=$PORT -Dhttps.proxyHost=$HOST -Dhttps.proxyPort=$PORT"
    GRADLE_OPTS="-Dgradle.user.home=$HOME/.gradle"
    MAVEN_OPTS=$JAVA_OPTS
    no_proxy="localhost,127.0.0.1,localaddress"
    echo "current proxy is ${http_proxy}"
    export no_proxy http_proxy HTTP_PROXY https_proxy HTTPS_PROXY all_proxy ALL_PROXY ftp_proxy FTP_PROXY dns_proxy DNS_PROXY JAVA_OPTS GRADLE_OPTS MAVEN_OPTS
}

setproxy
```
