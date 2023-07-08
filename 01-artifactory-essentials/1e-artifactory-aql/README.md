- [Artifactory AQL](#artifactory-aql)
  - [Sample Cmds](#sample-cmds)

# Artifactory AQL

## Sample Cmds

- ``` jf rt curl -XPOST api/search/aql -H 'Content-Type:text/plain' -d 'items.find({"repo":{"$eq":"example-repo-local"}})' ```

- ``` jf rt curl -XPOST api/search/aql -H 'Content-Type:text/plain' -d 'items.find({ "repo": "example-repo-local", "created": {"$last" : "40d"}, "stat.downloads": {"$eq" : null}})' ```


<br/>
<hr>
<br/>
