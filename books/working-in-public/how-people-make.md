## GitHub as a Platform

The chapter starts with a statement of the book's purpose:

> "This book is an attempt to identify, and expand upon, what it means to be online today, told through the story of open source, where individual developers write code consumed by millions."

Eghbal makes clear the scope within which she is examining open source:

- Primarily developers using GitHub
- Individual developers, rather than institutions or corporate actors
- Developers working in the United States, Europe, and Australia. She recognizes the significant open source work being done in countries like India and China, but the differences of behavior in those other countries caused her to limit her focus to "geographic regions that [she] can speak to more confidently"

### The Liberation of Code

Before code hosting platforms were ubiquitous people passed around tarballs, used mailing lists to communicate, and used different systems for collaboration depending on the project.

> "Much like visiting another country, if a developer wanted to contribute, they had to get up to speed on the local customs first:"

Git was released in 2005 by Linus Torvalds (developer of the Linux kernel), which replaced centralized version control systems (VCS) like [Subversion](https://en.wikipedia.org/wiki/Apache_Subversion) or [CVS](https://en.wikipedia.org/wiki/Concurrent_Versions_System). In contrast, Git provided a distributed VCS solution. Still, there was no consistent system from project to project.

Eghbal then dives into a discussion of the history of the free software movement, introducing [Richard Stallman](https://en.wikipedia.org/wiki/Richard_Stallman) and [Eric S. Raymond](https://en.wikipedia.org/wiki/Eric_S._Raymond). Stallman kicked off the free software movement at MIT in the '80s, and ESR was part of the first group of developers to embrace the term "open source."

Early open source developers believed that open source software was not owned by a single person, but rather owned in a more collective, associative sense. Quoting [Karl Fogel](https://en.wikipedia.org/wiki/Karl_Fogel), coauthor of Subversion:

> "When we say: 'that's my bike' or 'those are my shoes,' we mean that we own them. We have the final say in decisions about our bike. But when we say 'that's' my father' or 'my sister,' what we mean is we're associated with them[...]In open source, you can only have 'my' in the associative sense. There is no possessive 'my' in open source."

This historical attitude and perception of OSS resulted in a great deal of resistance toward adopting GitHub as a platform, especially because *GitHub's own code is not open source*.

### The Triumph of Convenience

GitHub was founded in 2008 by four Ruby developers, calling it a "social coding" platform. They immediately hitched their wagon to Git in the belief that it would be the future of software collaboration.

This obviously raises the question: how much of Git's rise to ubiquity has to do with GitHub's early adoption?

GitHub was preceded by Sourceforge, which was "more like a file-sharing site than a place to collaborate."

GitHub attempts to incorporate every part of the developer workflow into their platform. Issue tracking, pull requests (git merges), commit logs, developer profiles, etc.

GitHub also helped spread the use of more permissive licensing. 

The free software folks tended to use licenses like GPL, which require that all code using GPL-licensed software must also use the GPL license.

GitHub helped spread the use of licenses such as BSD and MIT, which allow developers to do pretty much whatever they want with the code.

Today the MIT license is by far the most popular, used by almost half of all GitHub projects.

> "GitHub's popularity among modern developers is the classic technology tale of convenience triumphing over personal values. To early free and open source developers[...]collaboration wasn't supposed to belong to anyone, and especially not to a multibillion-dollar company making proprietary software"

> "But the GitHub generation of open source developers doesn't see it that way, because they prioritize *convenience* over freedom[...]or openness[...]They just publish their code on GitHub because, as with any other form of online content today, sharing is the default."

As a platform, GitHub helped add value to software creators by extending their reach; improving their distribution. While developers are free to take their code elsewhere, there is a strong argument to be made for staying with GitHub because of the massive audience and ease of collaboration. 

Eghbal also points to the development of mature package managers (originally from the Linux ecosystem) as helping to extend the reach of the new wave of open source development. Package managers make sharing and consuming code extremely easy. The overhead with a tool like NPM is near-zero when it comes to distributing or consuming code.

### From Hackers to Huskies

Eghbal makes an interesting point about the relationship between JavaScript and GitHub:

> "Free software hackers define themselves by independence from platforms, but JavaScript might not have gotten as popular as it did without the advantages provided by a platform like GitHub, not to mention modern communication channels like Twitter and Slack. Unlike those who stress the freedom of code over all else, the JavaScript community exudes the opposite appeal: when code is small, it's the people who stand out."

Because JavaScript tools are so granular, a developer's identity is less tied to a specific project. This leads to a cult of personality, where all the projects that a popular developer works on gain attention by default (think Dan Abramov).

Maintainers of popular projects often maintain other projects as well, and can easily get overwhelmed by issues and PRs. Because GitHub makes it so easy to open issues, ask questions, open PRs, etc there is more of a revolving door of potential contributors who are likely not invested in sticking around long term.

### The GitHub Generation

GitHub's prominence could signal the death of "truly open" software development. More likely, **it indicates the importance of platforms to creators**.

> "Like every other social platform today, GitHub was designed for a use case that's breaking down at scale. Every platform must figure out how to adapt to an emerging set of social behaviors that is still not well understood."

## The Structure of an Open Source Project

The term open source really only describes how code is distributed and consumed. There is large variation in the organization, size, and community of different open source projects.

Eghbal makes the claim that there is no over-arching open source community, any more than there is an over-arching "urban community." Knowing your way around San Francisco doesn't help you much when you get to Hong Kong, apart from a general familiarity with what it takes to navigate a city.

### How Contributions Are Made

Anyone can propose a change to an OSS project by submitting a PR (a patch in other contexts than GitHub).

Contributions are subject to review, and must be approved by someone with permissions to merge changes.

Discussions around potential changes can range from informal conversations on issues or PRs to more formal RFC/proposal processes.

> "Despite impassioned rants to the contrary (if there's on thing I've learned, it's that developers have *opinions*), there's no one right way of doing things, just different communities that each have their own cultural norms."

### Where Interactions Take Place

OSS projects on GitHub are composed of three parts: code, an issue tracker, and pull requests.

Interactions around a project tend to take place:
- On GitHub
- Synchronous channels (IRC, Slack, Discord)
- Asynchronous channels (mailing lists, Reddit, GitHub issues)

### How Projects Change Over Time

#### Creation

One or a few developers, often work in a primarily closed manner, trying to get to an initial proof of concept. This is the stage where ideas are articulated and built on.

#### Evangelism

This is the stage where a project is promoted to others, as a means of getting feedback, bug reports, issues, and PRs.

The goal at this stage is distribution.

#### Growth

At this stage, a large part of the work is dealing with community interactions. Just the fact that a project is more popular does not mean that there are necessarily more people helping to maintain the project.

Typically projects enter at this stage into either a closed or distributed state.

In a **closed state** maintainers are more selective about external motivations and contributions, allowing them to focus on what they believe is the most important work

In a **distributed state** maintainers actively recruit help, hoping to maintain contributors in the project.

### Classifying Project Types

Eghbal identifies 4 main models of production: *federations, clubs, toys, and stadiums*.

#### Federations

These are projects with high growth of both contributors and users.

Rust, Node.js, and Linux are examples of federations.

More complex to manage, they tend to develop smaller working groups focused on smaller units of responsibility within the project.

#### Clubs

High contributor growth, but low user growth. 

Astropy is the example given: it's super useful for people using Python for astronomy, so those users tend to be pretty passionate about the project, but there aren't a huge number of people using Python for astronomy. This leads to lower user growth over time.

Similar to meetups or hobby groups&mdash;smaller reach, but loved and supported by enthusiasts.

Because of their relatively smaller size, the quality of members is important to the club. Most members ought to be contributors.

#### Toys

As the name implies, low contributor growth and low user growth. These tend to be side projects that an individual creates for fun.

#### Stadiums

Low contributor growth, but high user growth. This model is becoming increasingly common today.

Think webpack, Babel, Bundler, etc.

This model leads to more of a centralized community focused around the small group of contributors. This leads to a *one-to-many* social structure.

In a stadium, the creator is responsible for the basic structure of the group. Individual users have very little power.

Platforms like GitHub are essential for enabling stadiums. Here she seems to be making another argument for why creators need platforms such as GitHub.

## Roles, Incentives, and Relationships


The chapter starts with a statement of the book's purpose:

> "This book is an attempt to identify, and expand upon, what it means to be online today, told through the story of open source, where individual developers write code consumed by millions."

Eghbal makes clear the scope within which she is examining open source:

- Primarily developers using GitHub
- Individual developers, rather than institutions or corporate actors
- Developers working in the United States, Europe, and Australia. She recognizes the significant open source work being done in countries like India and China, but the differences of behavior in those other countries caused her to limit her focus to "geographic regions that [she] can speak to more confidently"

### The Liberation of Code

Before code hosting platforms were ubiquitous people passed around tarballs, used mailing lists to communicate, and used different systems for collaboration depending on the project.

> "Much like visiting another country, if a developer wanted to contribute, they had to get up to speed on the local customs first:"

Git was released in 2005 by Linus Torvalds (developer of the Linux kernel), which replaced centralized version control systems (VCS) like [Subversion](https://en.wikipedia.org/wiki/Apache_Subversion) or [CVS](https://en.wikipedia.org/wiki/Concurrent_Versions_System). In contrast, Git provided a distributed VCS solution. Still, there was no consistent system from project to project.

Eghbal then dives into a discussion of the history of the free software movement, introducing [Richard Stallman](https://en.wikipedia.org/wiki/Richard_Stallman) and [Eric S. Raymond](https://en.wikipedia.org/wiki/Eric_S._Raymond). Stallman kicked off the free software movement at MIT in the '80s, and ESR was part of the first group of developers to embrace the term "open source."

Early open source developers believed that open source software was not owned by a single person, but rather owned in a more collective, associative sense. Quoting [Karl Fogel](https://en.wikipedia.org/wiki/Karl_Fogel), coauthor of Subversion:

> "When we say: 'that's my bike' or 'those are my shoes,' we mean that we own them. We have the final say in decisions about our bike. But when we say 'that's' my father' or 'my sister,' what we mean is we're associated with them[...]In open source, you can only have 'my' in the associative sense. There is no possessive 'my' in open source."

This historical attitude and perception of OSS resulted in a great deal of resistance toward adopting GitHub as a platform, especially because *GitHub's own code is not open source*.

### The Triumph of Convenience

GitHub was founded in 2008 by four Ruby developers, calling it a "social coding" platform. They immediately hitched their wagon to Git in the belief that it would be the future of software collaboration.

This obviously raises the question: how much of Git's rise to ubiquity has to do with GitHub's early adoption?

GitHub was preceded by Sourceforge, which was "more like a file-sharing site than a place to collaborate."

GitHub attempts to incorporate every part of the developer workflow into their platform. Issue tracking, pull requests (git merges), commit logs, developer profiles, etc.

GitHub also helped spread the use of more permissive licensing. 

The free software folks tended to use licenses like GPL, which require that all code using GPL-licensed software must also use the GPL license.

GitHub helped spread the use of licenses such as BSD and MIT, which allow developers to do pretty much whatever they want with the code.

Today the MIT license is by far the most popular, used by almost half of all GitHub projects.

> "GitHub's popularity among modern developers is the classic technology tale of convenience triumphing over personal values. To early free and open source developers[...]collaboration wasn't supposed to belong to anyone, and especially not to a multibillion-dollar company making proprietary software"

> "But the GitHub generation of open source developers doesn't see it that way, because they prioritize *convenience* over freedom[...]or openness[...]They just publish their code on GitHub because, as with any other form of online content today, sharing is the default."

As a platform, GitHub helped add value to software creators by extending their reach; improving their distribution. While developers are free to take their code elsewhere, there is a strong argument to be made for staying with GitHub because of the massive audience and ease of collaboration. 

Eghbal also points to the development of mature package managers (originally from the Linux ecosystem) as helping to extend the reach of the new wave of open source development. Package managers make sharing and consuming code extremely easy. The overhead with a tool like NPM is near-zero when it comes to distributing or consuming code.

### From Hackers to Huskies

Eghbal makes an interesting point about the relationship between JavaScript and GitHub:

> "Free software hackers define themselves by independence from platforms, but JavaScript might not have gotten as popular as it did without the advantages provided by a platform like GitHub, not to mention modern communication channels like Twitter and Slack. Unlike those who stress the freedom of code over all else, the JavaScript community exudes the opposite appeal: when code is small, it's the people who stand out."

Because JavaScript tools are so granular, a developer's identity is less tied to a specific project. This leads to a cult of personality, where all the projects that a popular developer works on gain attention by default (think Dan Abramov).

Maintainers of popular projects often maintain other projects as well, and can easily get overwhelmed by issues and PRs. Because GitHub makes it so easy to open issues, ask questions, open PRs, etc there is more of a revolving door of potential contributors who are likely not invested in sticking around long term.

### The GitHub Generation

GitHub's prominence could signal the death of "truly open" software development. More likely, **it indicates the importance of platforms to creators**.

> "Like every other social platform today, GitHub was designed for a use case that's breaking down at scale. Every platform must figure out how to adapt to an emerging set of social behaviors that is still not well understood."

## The Structure of an Open Source Project

The term open source really only describes how code is distributed and consumed. There is large variation in the organization, size, and community of different open source projects.

Eghbal makes the claim that there is no over-arching open source community, any more than there is an over-arching "urban community." Knowing your way around San Francisco doesn't help you much when you get to Hong Kong, apart from a general familiarity with what it takes to navigate a city.

### How Contributions Are Made

Anyone can propose a change to an OSS project by submitting a PR (a patch in other contexts than GitHub).

Contributions are subject to review, and must be approved by someone with permissions to merge changes.

Discussions around potential changes can range from informal conversations on issues or PRs to more formal RFC/proposal processes.

> "Despite impassioned rants to the contrary (if there's on thing I've learned, it's that developers have *opinions*), there's no one right way of doing things, just different communities that each have their own cultural norms."

### Where Interactions Take Place

OSS projects on GitHub are composed of three parts: code, an issue tracker, and pull requests.

Interactions around a project tend to take place:
- On GitHub
- Synchronous channels (IRC, Slack, Discord)
- Asynchronous channels (mailing lists, Reddit, GitHub issues)

### How Projects Change Over Time

#### Creation

One or a few developers, often work in a primarily closed manner, trying to get to an initial proof of concept. This is the stage where ideas are articulated and built on.

#### Evangelism

This is the stage where a project is promoted to others, as a means of getting feedback, bug reports, issues, and PRs.

The goal at this stage is distribution.

#### Growth

At this stage, a large part of the work is dealing with community interactions. Just the fact that a project is more popular does not mean that there are necessarily more people helping to maintain the project.

Typically projects enter at this stage into either a closed or distributed state.

In a **closed state** maintainers are more selective about external motivations and contributions, allowing them to focus on what they believe is the most important work

In a **distributed state** maintainers actively recruit help, hoping to maintain contributors in the project.

### Classifying Project Types

Eghbal identifies 4 main models of production: *federations, clubs, toys, and stadiums*.

#### Federations

These are projects with high growth of both contributors and users.

Rust, Node.js, and Linux are examples of federations.

More complex to manage, they tend to develop smaller working groups focused on smaller units of responsibility within the project.

#### Clubs

High contributor growth, but low user growth. 

Astropy is the example given: it's super useful for people using Python for astronomy, so those users tend to be pretty passionate about the project, but there aren't a huge number of people using Python for astronomy. This leads to lower user growth over time.

Similar to meetups or hobby groups&mdash;smaller reach, but loved and supported by enthusiasts.

Because of their relatively smaller size, the quality of members is important to the club. Most members ought to be contributors.

#### Toys

As the name implies, low contributor growth and low user growth. These tend to be side projects that an individual creates for fun.

#### Stadiums

Low contributor growth, but high user growth. This model is becoming increasingly common today.

Think webpack, Babel, Bundler, etc.

This model leads to more of a centralized community focused around the small group of contributors. This leads to a *one-to-many* social structure.

In a stadium, the creator is responsible for the basic structure of the group. Individual users have very little power.

Platforms like GitHub are essential for enabling stadiums. Here she seems to be making another argument for why creators need platforms such as GitHub.

## Roles, Incentives, and Relationships

Our previous model for why people make things was based off of [Ronald Coase](https://en.wikipedia.org/wiki/Ronald_Coase)'s theory of the firm, which suggests that firms emerge naturally as a means of reducing transaction costs in the market. His theory implies that there is no reason for individuals to collaborate on OSS because the transaction costs are too high when compared with writing software with professional colleagues.
