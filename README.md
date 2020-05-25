# STATUS: WIP

# kobj

A Kubernetes CLI wrapper with object-first syntax.

A simple alternative to kubectl.

Makes it easier to perform series of operations on k8s API objects.


## Rationale

If you manage kubernetes clusters, you probably very often find yourself issuing seies of commands similar to this:

```
$ kubectl get po
$ kubectl get po myapp-9bf86f6a7-k6rn3 -o wide
$ kubectl describe po myapp-9bf86f6a7-k6rn3
$ kubectl logs myapp-9bf86f6a7-k6rn3
```

The annoying bit in this flow is that you have to navigate backwards through your last command to change the *verb*.
Here's how you would do the same with `kobj`:

```
$ kobj po
$ kobj po myapp-9bf86f6a7-k6rn3 get -o wide
$ kobj po myapp-9bf86f6a7-k6rn3 describe 
$ kobj po myapp-9bf86f6a7-k6rn3 logs 
```

That saves you a lot of keystrokes on the common tasks!


# Syntax summary

```
$ kobj <ObjectType> [get|list] [OPTIONS...]              - list objects of type ObjectType
$ kobj <ObjectType> <ObjectName> <Action> [OPTIONS...]   - perform Action on specified object
```

All the `OPTIONS` and `Actions` are the same as for kubectl. It really is just a simlpe wrapper around `kubectl`!


## Notes/Gotchas

There are a few deviations from how `kubectl` does things currently:
 - `logs` action still requires you to specify `po/pod/pods` as the `ObjectType`. This is for syntax consistency and to speed up the typical workflow.
 - `list` is introduced as an alias to `get`

## When to use `kobj`?

`kobj` is not written to replace`kubectl`, but rather to give you an alternative, object-focused perspective in situations where it's beneficial. So, as a rule of thumb:

 - If you're troubleshooting a single object or several of the same type, you'll be more effective with `kobj`
 - If you're exploring objects of various types, you'll be more effective with `kubectl`

## Bonus

Since it can be useful to alternate between `kobj` and `kubectl` perspective, `kobj` will always print the equivalent `kubectl` command at the bottom of the output, on stderr.
