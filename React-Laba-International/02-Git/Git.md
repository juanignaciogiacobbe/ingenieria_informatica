# <span style="color:#c00000">Git</span> 

## <span style="color:#c00000">Secure Shell(SSH)</span>

> Is a network communication protocol that enables two computers to communicate and share data.
> Is often used to "login" and perform operations on remote computers but it may also be used for transferring data.


## <span style="color:#c00000">Workflow </span>

![[Pasted image 20240422091819.png]]

## <span style="color:#c00000">Branches</span> 

> A branch is essentially a unique set of code changes with a unique name. Each repository can have one or more branches. The main branch - the one where all changes eventually get merged back into, and is called master.

![](https://lh7-us.googleusercontent.com/bilViwT8UnNXzylB0e9UZEDkOSVibDUJxNcR8vs_I0bhPyHjR7CDApeKqqxjn_lFWjrGSMQH0m2rexO7nsfpRYLszIp8BIQiQZxdNuHsAKf2sfEl5DqRE7Lv2EDgrktczlSRMntrcimHuvRusSX6syzegQ=nw)


## <span style="color:#c00000">Merge</span> 
> We can merge branches with help of git merge or git rebase command.
> The main difference is that the "merge" command does merge in one commit and "rebase" copies the full commits story while merging.

![](https://lh7-us.googleusercontent.com/PUi37LZHKX2vfNN9x564s2OBRDtzL-aZI6glkyRUF5uVexpqie1FckZH9EMVeaYhvhpzuG6WEv9vh_YY19bgc51I16XE3ynUJ_4mDlM7jEqG5l7A3ja_PFIJq204B7ksntR5IIH_aSEai2Jvoda1DH3vyA=nw)

![](https://lh7-us.googleusercontent.com/3le5Y6C0HTWRh6m1iLlf-X7jz-2QRiNx_tXWcrA6djd8MuqsLGTtW5pq1_7Yn6pjGyKvvcFX23HSAs15Akk9mbU-K6-V8zzIvi6M9YVusX8OtLUVWjq38I6rgTwzGJEMyVQtr2FEvFw1cCOn3rCC619X-g=nw)


### <span style="color:#c00000">Rebase use</span> 

><span style="color:#ffff00">After the rebase is completed, Git creates new commits with new ids, then permanently deletes the old commits</span>. If other users are working on branches that came from the deleted commits, they can’t push their changes back to their origin.

![](https://lh7-us.googleusercontent.com/5sIYj35jznzZ8Exw-LQDw4Z0Q7_onNBTiD-MJOabroX8QmBGZmv7QfMkOZPp_c_C1-86AWzvfZHVeFtDh6NtkniS-xjpjIGVT9dItkWkqo8V-a1vvJ_dlZZA-Ws2HHJHjEr64ZHndxlCCI78Q5iI7_tzLA=nw)