---
published: true
---
## Docker error, no space left on device

### typical solution:
`docker system prune [-af]`  
this deletes all the containers and images used/unsued depening upon flags passed.

##‭# better solution
use `.dockeringore` and reduce docker build context.  

With each docker build, by default, the entire directory is sent to Docker's build context which in my case was more than `300MB` of data. This was eating up docker's default 12 GB space several times within a week.  

But docker doesn't really need all the files in the repository for building the final containers, especially the `.git` folder, the test files and other test and deployment resources.  

To avoid sending those resources, we can use `.dockerignore` file and add unnecessary files and folders like a `.gitignore` file. This way, i was able to reduce the size of build context from `300+MB` to just `27MB`.  

You would surely hit your docker space limit at some point, but that point just got months away.
