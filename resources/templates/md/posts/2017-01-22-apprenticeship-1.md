{:title "Table XI Apprenticeship"
 :layout :post
 :tags ["apprenticeship" "tablexi" "ruby" "rails" "agile"]}

I am nearing the end of my apprenticeship with Table XI, and I wanted to
take the opportunity to reflect on a wonderful six months during which I
learned a ton. I am deeply grateful to the outstanding team—in
particular my coaches John and Pete and my fellow apprentice Zino.

### Applying

I had applied and been accepted into a different company’s
apprenticeship program earlier this year. As the start date of August 1
neared, that company realized that its business needs had changed, and
so was forced to rescind the offer. I was disappointed, but was thankful
that they put me in touch with Table XI, which was then putting together
its inaugural apprenticeship class, slated to start August 15.

I visited Table XI and was then sent their coding challenge. The coding
challenge has since changed (and the old one is easily discovered by
searching GitHub), so here’s my
[code](https://github.com/Ethan826/tablexi-coding-challenge) from the
challenge. It was good enough, so I was called back for a day of
interviewing and pair programming (and the Lego
[game](http://www.tablexi.com/clients/learn-agile-with-lego/)). A week
or so later, I got an offer to become an apprentice.

### Beginnings

I am a self-taught developer whose previous experience was a mile wide
and an inch deep. Zino, the other apprentice, completed two years of a
computer science degree, worked in tech companies, and graduated from
Dev Bootcamp in New York before coming to Table XI. So tailoring the
program was a must, and has been a focus of the program’s first
iteration.

Table XI assigned each of us two coaches—one a more senior developer,
the other more junior. In the first week, we worked through the new
coding challenge (sorry, can’t tell you about that one). Zino blasted
through it, while it was the most complicated Rails app I had worked on,
and so a great way to start learning Table XI’s preferred stack.

Next, we began building Delivery Dashboard, a portal now used internally
by our project managers to track projects. It gathers subjective data
from team surveys as well as objective data from Pivotal Tracker (used
to track chunks of work called “stories” in agile parlance), Harvest
(timekeeping software), and other data sources.

At the same time, my coaches and I read through <i>Agile Web Development
with Rails 5</i> a chapter at a time, reviewing it during our daily
check-in sessions. When we finished that, we read through <i>99 Bottles of
OOP</i>, meeting every few days to discuss our thoughts. I also did
numerous exercises on [exercism](http://exercism.io/Ethan826) and
watched a lot of the Ruby Tapas videos.

### Client work

Within a few weeks, we were put on a small client matter. Our client
generates a huge amount of data in the form of numerous log files. Our
job was to write a gem to ingest those files and a control file, process
the data, create charts through the HighCharts API, build those charts
into HTML, then convert them to PDF through the DocRaptor API.

Later I got to work on encrypted log files, which were being decrypted
by C\# code. The key used for decryption wouldn’t work in Ruby (the
Rijndael library in C\# will pad a key in a way we weren’t able to
replicate in Ruby). So I got to roll up my sleeves and write some C\#
code, called by Ruby, run in Mono on my Mac. That was fun.

### Meetup

As the program continued, Zino and I were invited by Amelia from the
Apprenticeship Meetup and Trunk Club to speak at an
[event](https://www.meetup.com/Chicago-Apprenticeship-Meetup/events/235664341/).
I enjoyed the opportunity and was glad that several of the attendees
came to have lunch with us in the next few weeks (Table XI serves lunch
every day, and is very welcoming of guests interested in the company).

### More client work

In the past few months, the focus has shifted to Zino and my working
mostly on client projects. First, I worked on a gem that runs a cron job
to retrieve data from a large database, then push it to the GeckoBoard
API to power a dashboard in our client’s office.

Next, Zino and I both worked on a Rails app that provides dietary and
lifestyle support services to organizations serving people with
developmental disabilities. The changes were relatively simple, but
touched big chunks of our first “real world” legacy application,
comprising over 10,000 lines of code.

We are now working on a Rails app that provides proprietary analysis of
financial institutions to subscribers. The application comprises over
30,000 lines of code. It’s well organized and tested, follows best
practices, and uses numerous common gems. It also has some tricky bits,
like multiple-table inheritance, text searching, and a rather complex
data model. I have worked on stories involving changes to several data
models (changing how users and admins can view, create, and update
lists). I paired extensively with a senior dev and have learned a lot.

Getting to play the role of a junior dev has been exciting. I’m pleased
to find that I’m able to contribute to a large app. I had worried that I
wouldn’t be able to understand how the whole thing worked in detail, but
the skill in working on a large project seems to be isolating the
portion you need to understand in order to implement the feature you’re
working on. Over time, you start to grok how the whole app works. As you
gain experience overall, I think you get better at comprehending the
whole more quickly based on pattern recognition. But it’s empowering to
realize that even as a newbie, you can use systematic experimentation to
understand how a chunk of functionality works, and figure out where and
how to make the change you’ve been assigned.

I have also benefitted from working on an agile team, complete with
IPMs; storytime; project tracking with Pivotal Tracker and Redmine; VCS
with GitHub, CircleCI, and PR-based workflow; etc. That’s the kind of
thing that’s impossible to gain experience with outside of actual
project work, and has been almost as important to building my skills as
the coding itself.

So to has been the emphasis on the clients’ business needs. Building
software is a means, not an end: Table XI is a consultancy whose role is
to help clients solve <i>business</i> problems. It just so happens that
clients most often come to us with business problems for which custom
software is the best solution. But when it isn’t, we tell them, because
our long-term relationships are more important than selling any
particular project.

### Conclusion

The past 5-1/2 months have been interesting, demanding, challenging, and
enormously satisfying. Two roads diverged in a wood, and I—I took the
one that led to a career that makes me feel excited and fulfilled (not
to mention the one that pointed the hell away from practicing law). And
that has made all the difference. Really!

I look forward to deepening and broadening my skills and continuing to
have a job that pays me to do something I do for fun anyway. I’m very
grateful to Table XI for the opportunity, and I look forward to the next
step, whether it’s becoming a full-time dev there or somewhere else.
