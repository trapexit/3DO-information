# Why 'iamaduck'?

If you look at the data on a 3DO CDROM you'll notice the ASCII values for 'iamaduck' over and over. On 1994-08-27 Dave Platt who worked at The 3DO Company at the time posted the following to [rec.games.video.3do](https://groups.google.com/forum/#!msg/rec.games.video.3do/00Q4m8y_2wE/RSmVsilumb0J).

```
Newsgroups: rec.games.video.3do
Path: bga.com!news.sprintlink.net!hookup!news.kei.com!eff!news.duke.edu!news-feed-1.peachnet.edu!emory!swrinde!elroy.jpl.nasa.gov!decwrl!ditka!ntg!dplatt
From: dpl...@3do.com (Dave Platt)
Subject: Re: Why 'iamaduck'?
Message-ID: <1994Aug27.191537.17055@ntg.com>
Sender: ne...@ntg.com (USENET news account)
Organization: The 3DO Company Inc., Redwood City CA
References: <Cv5sq0.6Hn@oucsace.cs.ohiou.edu>
Date: Sat, 27 Aug 1994 19:15:37 GMT
Lines: 66

>  A while ago, a wise man came from on high carrying two stone CDs. He
>declared that the 3DO uses the preinitialization string 'iamaduck' to
>signify that the space on the CD is unused.

Usually so, although the init string can be overridden during the CD-ROM
layout/premastering process.

>                                       He then asked if anyone knew
>of the origins of this string, or another OS that uses it.  There was a
>great silence...  I have come to break that silence. 
>
>  "Nope.  What's the answer?"       = )

OK - it's been about six months, and nobody has been able to identify
where I got this string from (not enough old-timers around, I guess).
So, I'll reveal it.

The use of this string "iamaduck" is sort of a homage to one of first
"real" operating systems I ever had a chance to hack with.  It was the
CP-V (Control Program 5) operating system, which ran on the Xerox
Sigma-6 (and later) 32-bit mainframes.  This OS (and its predecessor
UTS) was an extremely flexible multiuser OS, which handled both batch
jobs (typically submitted from cards), on-line interactive users, and
"ghost" jobs (what a Unix person would call a daemon).  It was written
to run in a small-memory environment, by today's standards - a 256k word
(one-megabyte) CP-V system was larger than usual - and it was capable of
supporting dozens of interactive users (on Teletypes or equivalent ASCII
terminals) and running several batch jobs, all at once.  It normally
used a high-speed fixed-head disk or drum as a swap device.

The string IAMADUCK was used in the CP-V operating system to
pre-initialize an error recording table known as the "75TABLE".  This
table was used as a snapshot area, to record any inconsistencies in the
filesystem data structures (in memory or disk) which were detected at
runtime.  Such filesystem errors (e.g. lost or inaccessible files) were
reported to the program via a standard CP-V four-hex-digit error code
beginning with the sequence 75 (e.g. 7514 means "Cannot access file due
to directory damage")... hence the name of the 75TABLE array.

Since the 75TABLE was preinitialized to a repeated series of IAMADUCK,
and was of a known fixed size, it was easy to tell whether any
filesystem errors had been detected by simply glancing at a hex/ASCII
dump of that portion of the kernel's memory region.  If you didn't see
the usual number of lines of IAMADUCK, you knew that there was some
filesystem trace information in the array which was worth examining.

When I wrote the 3DO CD layout software, I decided that preinitializing
the CD image file would be a Good Thing, to help debug problems,
identify uninitialized storage at runtime, and ensure that the old
contents of the image file wasn't accidentally mastered onto a CD
(remember the Prodigy STAGE.DAT file furor?  Same issue...).  I decided
to resurrect an identifying string from the first real filesystem code I
ever played around with.

Now... why did CP-V use "IAMADUCK" as its logging initializer?  Beats
me.  I never knew who wrote that code (although I did work with many of
the CP-V developers after their move to Honeywell during the development
of the CP-6 O/S).

So... the secret is now out, and the offer of bonus points for answering
the question has hereby expired.
--
Dave Platt    dplatt@3do.com
      USNAIL: The 3DO Company, Systems Software group
              600 Galveston Drive
              Redwood City, CA  94063
```
