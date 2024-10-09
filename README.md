In cachyOS there's cachyos-settings which is pretty clutch/core to whats going on there - so  gotta keep it

but something happened and then i had to give up ananicy-cpp but that was hooked to the cachyos-settings so i was stuck to disable and remove the value from the ananicy-cpp.service file's WantedBy= part and see why or what was causing it to need version 10 and why i had version 11 - focused on finding the 10 not the why part out


So basicallly I tried to repackage a 10.0.0 but really just muddled my way through doing the standard thing which is to write a PKGBUILD which I knew very little about or forgot more than i ever knew I had known.

Then I found aur/downgrade - which is seemingly working with ALA or archive arch linux website - like a beauty too - but still want to upload what I have because for learning
Im tryin gto make --check the source directly i have but its failing so I could have probably  just downloaded the original tar baall and tried make --check then and itd be okay idk what ive been doing  progress wise but with duck duck go's AI helping me learn I managed to learn a few things I didn't know i dont think


``
   10.0.0.tar.gz ... FAILED
==> ERROR: One or more files did not pass the validity check!
``

But ya check out aur/downgrade its pretty mondo - towards the end of 'rebuilding' a PKGBUILD file just or learning as it were I wondered if a downgrade package existed it does totally

So then i looked into what might happen what depeneded on <h3>fmt</h3>  that might blow up if I downgraded it - bunch of new intel one-api guys and a mcmap ??  smh

not sure but proabbly thought they were cool at the time or got un-intentionally installed - the mcmap i think i did myself bc it sounded cool 

the oneapi intel stuff i dont think i would have consciously done bc of my experience with them in the past  im amd cpu / gpu guy btw


so thats about it cheers
