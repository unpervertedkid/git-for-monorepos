# Monorepo

## What is a monorepo

There exist many definitions of what a monorepo is. I will try to put together all the different definitions and explain them in a way that makes sense to me. I will not argue about whether you should or should not use a monorepo, that as always depends on your specific use case, but I will try to explain what a monorepo is and what it is not.

The following are some of the definitions I found:

- A monorepo is a single repository containing `multiple distinct projects`, with `well-defined relationships` -[Nrwl][1]
- A monorepo is a version-controlled code repository that holds `many projects`. While these projects may be related, they are often `logically independent and run by different teams`.[Tomas Fernandez][2]
- A monorepo is a `large` and complex repository, containing multiple logical projects that are `either unrelated, loosely connected, or connected` by other means such as dependency management tools, and having a `high number` of commits, branches, tags, files, and content size.[Attlasian][3]

From the above definitions, we can agree on what a monorepo is:

- A monorepo may contains multiple projects
- The projects in a monorepo may either be unrelated, loosely connected, or connected by other means such as dependency management tools
- The projects in a monorepo may be  logically independent and run by different teams
- A monorepo is large and complex

### What a monorepo is not

#### ⚠️ Monorepo ≠ Monolith

A common misunderstanding is that having a monorepo means deploying all applications together, similar to a monolith. However, the place of code development and the timing of deployment are separate concerns. For example, Google has thousands of applications in its monorepo, but they are not all released simultaneously. Good CI/CD practices separate the build and storage of artifacts during CI from their deployment. Therefore, adopting a monorepo can actually increase deployment flexibility due to simplified code sharing and cross-project refactoring.[Victor Savnin][4]

#### ⚠️ Monorepo ≠ Just Code Colocation

 A monorepo is not simply a repository with several projects in it (code colocation). If there are no well-defined relationships among the projects, it's not a monorepo. Similarly, a repository containing a large application without division and encapsulation of discrete parts is just a big repo, not a monorepo. A good monorepo is the opposite of monolithic, promoting division and encapsulation of parts.[Nrwl][5]

## But Why?

The standard way of developing applications today is using a "polyrepo", where each team, application, or project has its own repository. This approach provides team autonomy over their libraries, deployment schedules, and contributors. However, this autonomy comes at the cost of isolation, which can hinder collaboration. Drawbacks of a polyrepo environment include:

1. **Cumbersome code sharing**: Sharing code across repositories often requires creating a separate repository for the shared code, setting up tooling and CI environments, adding committers, and setting up package publishing. Reconciling incompatible versions of third-party libraries across repositories can also be challenging.

2. **Significant code duplication**: To avoid the hassle of setting up a shared repo, teams often write their own implementations of common services and components in each repo. This not only wastes time upfront but also increases the burden of maintenance, security, and quality control as the components and services change.

3. **Costly cross-repo changes to shared libraries and consumers**: Fixing a critical bug or making a breaking change in a shared library requires setting up environments to apply changes across multiple repositories with disconnected revision histories. Coordinating versioning and releasing packages can also be a significant effort.

4. **Inconsistent tooling**: Each project uses its own set of commands for running tests, building, serving, linting, deploying, etc. This inconsistency creates mental overhead as developers need to remember which commands to use from project to project.

Note: Most of this has been largely adopted from [Nrwl][6]

## The Good, The Bad, and The Ugly

Just like any decision in software engineering, the decision on whether to use or not use a monorepo is a decision(often a hard one) on whether the balance of the good, the bad, and the ugly is in your favor.

Monorepos therefore have their own good, bad, and ugly sides.

### The Good

Monorepos offer several advantages:

1. **Code Accessibility**: All code is in one place, simplifying the process of finding and changing code across multiple repositories.
2. **Ease of Refactoring**: Large-scale refactors are easier to implement as all changes can be part of one pull request, merged and deployed at the same time.
3. **Simplified CI/CD**: Monorepos make working with CI/CD systems easier as the entire project can be spun up to run tests or other tasks.
4. **Dependency Sharing**: Managing dependencies is easier in a monorepo as all code is in one place, reducing the complexity of updating dependencies across multiple repositories.
5. **Visibility**: Everyone can see all the code, leading to better collaboration and cross-team contributions.
6. **Single Source of Truth**: One version of every dependency prevents versioning conflicts and dependency hell.
7. **Consistency**: Enforcing code quality standards and a unified style is easier with all code in one place.
8. **Shared Timeline**: Breaking changes in APIs or shared libraries are exposed immediately, promoting communication and collaboration among teams.
9. **Atomic Commits**: Large-scale refactoring is easier with atomic commits that can update several packages or projects in a single commit.
10. **Implicit CI**: Continuous integration is guaranteed as all the code is unified in one place.
11. **Unified CI/CD and Build Process**: The same CI/CD deployment process and build process can be used for every project in the repo.

### The Bad

Monorepos also have several drawbacks:

1. **CI/CD Challenges**: Large monorepos can lead to slower CI/CD pipelines, affecting developer productivity and potentially increasing costs.
2. **Complicated Builds**: Building different parts of a monorepo in the correct order can be complex, compared to building the entire repository at once.
3. **Team Communication**: With everyone working in one repo, clear communication becomes crucial to avoid conflicts and ensure effective review of large pull requests.
4. **Design Limits**: As monorepos grow, they can hit design limits in version control tools, build systems, and CI/CD pipelines.
5. **Performance Issues**: Scaling up monorepos can lead to performance issues, such as slow commands and lagging IDEs.
6. **Risk of Broken Master**: A broken master affects everyone working in the monorepo, which can be disastrous if not managed properly.
7. **Steep Learning Curve**: New developers may face a steeper learning curve if the repository spans many tightly-coupled projects.
8. **Large Volumes of Data**: Monorepos can reach unwieldy volumes of data and commits per day.
9. **Ownership Challenges**: Maintaining ownership of files can be more challenging in a monorepo, as systems like Git or Mercurial don’t feature built-in directory permissions.
10. **Code Reviews**: Notifications can get very noisy, especially on platforms like GitHub that have limited notification settings.

## So, When Should you consider using a monorepo?

Consider using a monorepo when:

1. **Code Sharing and Collaboration**: You have multiple projects with interdependencies and you want to promote code sharing and collaboration.
2. **Simplified CI/CD**: You want to simplify your CI/CD pipeline by having all code in one place.
3. **Refactoring**: You frequently perform large-scale refactors that span across multiple projects.
4. **Single Source of Truth**: You want to maintain a single source of truth for your codebase and dependencies.
5. **Code Visibility**: You want to increase code visibility across teams.

However, be aware of the potential challenges such as CI/CD complications, complex builds, the need for clear team communication, design limits, performance issues, risk of a broken master, steep learning curve for new developers, large volumes of data, ownership challenges, and noisy code reviews.

## References

[1]: https://monorepo.tools/#what-is-a-monorepo:~:text=A%20monorepo%20is%20a%20single%20repository%20containing%20multiple%20distinct%20projects%2C%20with%20well%2Ddefined%20relationships.
[2]: https://semaphoreci.com/blog/what-is-monorepo#:~:text=A%20monorepo%20is%20a%20version%2Dcontrolled%20code%20repository%20that%20holds%20many%20projects.%20While%20these%20projects%20may%20be%20related%2C%20they%20are%20often%20logically%20independent%20and%20run%20by%20different%20teams.
[3]: https://www.atlassian.com/git/tutorials/monorepos#:~:text=Monorepos%20in%20Git-,What%20is%20a%20monorepo%3F,-Definitions%20vary%2C%20but
[4]: https://blog.nrwl.io/misconceptions-about-monorepos-monorepo-monolith-df1250d4b03c#:~:text=Misconceptions-,Monorepo%20!%3D%3D%20Monolith,-Will%20we%20have
[5]: https://monorepo.tools/#what-is-a-monorepo:~:text=Not%20just%20%E2%80%9Ccode%20colocation%E2%80%9D
[6]: https://monorepo.tools/#why-a-monorepo