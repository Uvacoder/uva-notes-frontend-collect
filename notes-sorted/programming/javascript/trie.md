```
function contacts(queries) {
    const trieRoot = {}, ans = [];
    queries.forEach(([qType, str]) => {
        let curr = trieRoot;
        if(qType === 'add') {
            for(const ch of str) {
                if(!curr[ch]) curr[ch] = { count: 0 };
                curr = curr[ch], curr.count++;
            }
        } else {
            for(const ch of str) {
                if(curr[ch]) curr = curr[ch];
                else { ans.push(0); return; }
            }
            ans.push(curr.count);
        }
    });
    return ans;
}
```
