# triage get-states

The **triage get-states** command retrieves the available triage states for a given scan type, including custom states.


{% hint style="info" %}
Custom states is only available for accounts that have Phase 1 of the new Access Management.
{% endhint %}


## Usage
```
./cx triage get-states [flags]
```


## Flags
**`--all`**

Show all custom states, including the ones that have been deleted.

**`--help`**

Help for the triage get-states command.


## Examples
Sample command:

```
user@laptop:~/ast-cli$ ./cx triage get-states
```

Sample response:

```
[{"id":13651,"name":"custom-state-4269583488125138725","type":"INFO"},{"id":13684,"name":"custom-state-7065983805428327353","type":"INFO"},{"id":13717,"name":"custom-state-8841123802087642575","type":"INFO"},{"id":13752,"name":"custom-state-271808954341294024","type":"INFO"},{"id":13785,"name":"custom-state-4318314140970845122","type":"INFO"},{"id":13821,"name":"custom-state-5130643464138548710","type":"INFO"},{"id":13718,"name":"custom-state-2286071310219315628","type":"INFO"},{"id":13786,"name":"custom-state-8692272966226908953","type":"INFO"},{"id":13822,"name":"custom-state-1072205568533198574","type":"INFO"},{"id":14094,"name":"dsfd","type":"INFO"},{"id":13719,"name":"custom-state-296535314730089576","type":"INFO"},{"id":13925,"name":"sdjb","type":"INFO"},{"id":13788,"name":"daniel","type":"INFO"},{"id":13926,"name":"aa","type":"INFO"},{"id":-1,"name":"TO_VERIFY","type":""},{"id":-1,"name":"NOT_EXPLOITABLE","type":""},{"id":-1,"name":"PROPOSED_NOT_EXPLOITABLE","type":""},{"id":-1,"name":"CONFIRMED","type":""},{"id":-1,"name":"URGENT","type":""}]
```

