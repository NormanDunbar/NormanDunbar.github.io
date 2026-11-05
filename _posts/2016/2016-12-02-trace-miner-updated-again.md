---
title: Trace Collier Utility - Updated
date: 2016-12-02
layout: post
---

> When originally written, `Trace Collier` was named `Trace Miner`. However, after a "cease & desist" from lawyers for a bigger than me company, Synaxus in Germany, I had to change it.

Trace Collier has been updated after a couple of foibles were found during the processing of a trace file.

The version has been bumped to 0.19 as of today, 2nd December 2016. The bugs fixed were:

- The utility now notices exec `ERROR` lines as well as `PARSE ERROR`s. Just because it's nice to know where things might have gone wrong. These are in addition to the `PARSE ERROR`s that it has been processing up until now.
- Interesting bug, seemingly related to `DBMS_METADATA.GET_CLOB` calls where the value for one bind is the bind number of the next one. The text in the trace file is `value= Bind#` and is weird! It should be on two lines, everything after the equals sign, including the space, should be on the next line. Detected on Windows 11204 and on Solaris 11204.
- Sort of fixed the problem where a bind can be used more than once in a statement. Flagged in the SQL as `__A_:BIND_REUSED__` at the moment. This will be properly fixed in future but where the same bind variable is used more than once in a statement, the code now (sort of) handles it correctly. An issue has been raised on GitHub for this.
- Added `test.cmd`. Test harness for Windows users.

You can read more about [Trace Collier](/2016/02/26/trace-miner-an-oracle-utility/) here if you wish.
