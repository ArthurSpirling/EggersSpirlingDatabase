# Eggers and Spirling British Political Development database, 1802--2010

## Download
The compressed database in CSV format (634M) is available [here](http://andy.egge.rs/data/csv_archive_20150612.zip) (last updated in June 2015).

## Overview
The dataset consists of roll call votes, election returns, and speeches linked to MPs over the period 1802-2010. The speeches cover the period 1832-1918; the votes cover the period 1836-1910; the elections cover the period 1802-2010 (although they are not linked consistently to MPs after 2001 yet).

## Citation
Users of the dataset should cite the Eggers and Spirling LSQ article:


> Eggers, Andrew C., and Arthur Spirling. "Electoral security as a determinant of legislator activity, 1832–1918: New data and methods for analyzing British political development." Legislative Studies Quarterly 39.4 (2014): 593-620.

They should also see that article for details on how the data was assembled.

BibTex: 
```
@article{eggers2014electoral,
  title={Electoral security as a determinant of legislator activity, 1832--1918: 
  New data and methods for analyzing british political development},
  author={Eggers, Andrew C and Spirling, Arthur},
  journal={Legislative Studies Quarterly},
  volume={39},
  number={4},
  pages={593--620},
  year={2014},
  publisher={Wiley Online Library}
}
```

## Data structure
MPs are identified in the file mps.csv. The unique key is the first column, labeled "member_id". Other files (detailing the votes, electoral records, and speeches of MPs) refer to member_id when they identify an MP.

### Elections

Elections are described in two sheets -- elections.csv and election_returns.csv.

- In **elections.csv**, each row describes an election contest, which is an event in which several candidates compete for one or more seats in a constituency. The information includes the name of the constituency, the number of electors, the date, an indicator for by-election, number of seats in the constituency, number of seats being contested, and sometimes some notes. The unique key in this table is election_id.

- In **election_returns.csv**, each row describes a single election return, which is the experience of one candidate competing for a seat in an election contest. The information includes the name of the candidate, the party listed, an indicator for whether the return was unopposed, the number of votes, and an indicator for whether the candidate was a winner (which sometimes differs from the vote count due to the decision of an election petition). It also includes two "foreign key" columns: election_id identifies the election in which this return appeared, and member_id identifies the MP for all successful candidates.

###  Division Votes
Division votes (i.e. roll call votes) for a given parliament are described in two sheets found in divisions_by_parliament.

- In **divisions_parliament_X.csv**, each row describes a division, which is an event in which several members vote on a question, that took place in parliament X. The unique key is labeled "id". Other information includes the date, the name of the History of Parliament Trust file in which the division was digitized, and the text of the question as it appeared in the Division Lists.

- In **votes_parliament_X.csv**, each row describes the voting record of one MP in the divisions that arose in a given parliament X. The mp is identified by a column labeled "mp.id" (which corresponds to the "member_id" column in mps.csv); we also provide some of the information from the mps.csv table along with a record of the MP's party at the start (90 days after the election) and end (30 days before the next election) of the parliament; this record is based entirely on the election records reported in election_returns.csv. There is then a column for each division; if the column is labeled "d4449", that means that you can recover the content of the division by looking up the division with id of 4449 in divisions_parliament_X.csv.
In addition, we provide the raw votes and details on every division in two CSV files found in raw_votes_and_divisions. Note that these include divisions we imported from Valerie Cromwell's datafiles and from Aydelotte's dataset; these divisions are duplicated in the 1836-1910 data we got from the Division Lists (digitized by the History of Parliament Trust).

- In **cohesion.csv** [here](https://www.dropbox.com/sh/cftvjx57jhfue83/AACn88LhvXXCfKV6iLCcZZK-a?dl=0), we provide (for each MP/for each parliament) a measure of their "cohesion".  This is essentially how often (as a proportion of all divisions, 0 to 1) they voted the same way as their party whip.  This is not part of the original Eggers and Spirling Dataset, but rather something derived from it and that appeared in the following paper:


```
@article{eggers2016party,
  title={Party cohesion in Westminster systems: inducements, replacement and discipline in the house of commons, 1836--1910},
  author={Eggers, Andrew C and Spirling, Arthur},
  journal={British Journal of Political Science},
  volume={46},
  number={3},
  pages={567--589},
  year={2016},
  publisher={Cambridge University Press}
}
```



### Speeches
Speeches for a given parliament are described in two sheets found in speeches_by_parliament.

- In **debates_parliament_X_elected_Y.csv**, each row describes a debate, which is a collection of speeches, that took place in parliament Y. We provide the date of the debate, the title as reported in the digitized Hansard, and the location of the debate in the digitized Hansard.
- In **speeches_parliament_X_elected_Y.csv**, each row describes a speech, which is a set of words spoken by a member in the House of Commons. We provide the xml_location of the speech, the raw name of the speaker, the member_id matched to this speech (when possible -- note that the matching is patchy before 1832), the date of the speech, the id of the debate (linking to debates_parliament_X_elected_Y.csv), and the body of the speech.

It should be clear that in each case (elections, divisions, debates) there is a nesting structure: each election has many returns; each division has many votes; each debate has many speeches. And in each case the unique ids in the higher-level object appears in the entry for the lower-level object.

### Constituencies and Office holding
We also provide (as of version 1.1):

- **constituencies.csv**, which provides background on the constituencies referenced by constituency_id in e.g. elections.csv
offices.csv, which is a list of offices MPs held
- **officeholdings.csv**, which references offices and MPs, specifying when particular offices were held by particular MPs
services.csv, which references constituencies and MPs, specifying when particular MPs held particular seats

## Corrections
Corrections/improvements are welcome. Best is if you can provide us with a new version of a CSV with corrections or additions made and documented.

Thank you!

[Andy Eggers](http://andy.egge.rs/) and [Arthur Spirling](http://www.nyu.edu/projects/spirling/)

