# PoolParty (PPT) frontend (FE) customisation

This is the customisation for http://joinedupdata.org. Below is a list of the approached we took in order to customise the PPT FE, left here for informational purposesed. I think that we've managed to get it to 'stick'. We'll see what happens after the upgrade of the web app.

---

### Take \#1

I noticed that with the current PoolParty version (the live one, Version 5.4.1, revision 10614) the default (/opt/poolparty/data/frontendRoot/default) directory where the files in this repo sit, doesn't get rebuilt when PPT restarts as before. This means we can simply replace the current default folder.

---

### Take \#2

It looks like PPT rebuilds **both** of the two folders in `/opt/poolparty/data/frontendRoot/` i.e., `custom` & `default`. Therefore, to make the customisations live, it was necessary to delte the `custom` folder and to replace the `default` folder when PPT is on. We have not tested the behaviour after a restart. There is a possblity that the customisation will again be wiped after a restart. If so, should this be looked into? It's not sustainable for us to redo this every time we reboot the software.

---

### Take \#3

It has been confirmed that the customisation gets wiped after a restart. The advice from the Semantic Web Company regarding this issue is: 

> Using the custom folder for your LD frontend customization keeps the CSS customizations, even when the server is restarted or re-deployed e.g., during an update.

I am pretty sure we tried that and that it did not work (see above).

There is more information here: https://help.poolparty.biz/faq/faq-s/operating-poolparty-server/how-to-set-up-a-custom-linked-data-frontend.

---

### Final take?

1) Stop the web app

2) Back up the working installation

3) Place all customisation in `.../frontendRoot/custom/`

4) ```cd .../frontendRoot/custom/```

4) Replace references to the `default` folder with references to the `custom` folder:
```
grep -rl 'default' . | xargs sed -i "s|default/|custom/|g"
```

5) Start the web app...

... and the customisation should stick.
