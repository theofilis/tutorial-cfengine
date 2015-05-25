# Promise States

CFEngine defines the following promise states:

<dl>
	<dt>
		<strong>Promise kept</strong>
	</dt>
	<dd>
	The state of the system was already as described by the promise, so no action had to be taken.
	</dd>
	<dt>
		<strong>Promise repaired</strong>
	</dt>
	<dd>
The state of the system was not as required by the promise, so CFEngine took the
appropriate actions, and repaired the system state to match the requirements of
the promise.
	</dd>
	<dt>
		<strong>Repair failed</strong>
	</dt>
	<dd>
Repair actions were attempted by CFEngine, but they failed for some reason (for
example, lack of permissions to edit a file).
	</dd>
	<dt>
		<strong>Repair denied</strong>
	</dt>
	<dd>
Repair actions were attempted by CFEngine, but they failed due to lack of access
to some resource. (In the current version of CFEngine, this status is set only when
CFEngine fails to change the owner or BSD flags of a file, or when it fails to touch it.
	</dd>
	<dt>
		<strong>Repair timeout</strong>
	</dt>
	<dd>
		Repair actions were attempted by CFEngine but took too long to execute, and
CFEngine cancelled the operation.
	</dd>
</dl>