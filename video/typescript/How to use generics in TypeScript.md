# How to use generics in TypeScript

- https://www.youtube.com/watch?v=t0qQSujSslQ&list=WL&index=3

## ex) job queue examples

```
type Job = {
	name: string;
	start: () => void;
	state: 'incomplete' | 'success' | 'failure';
}

type JobRun<J extends Job> = {
	job: J;
	state: 'queued' | 'running' | 'completed';
	onComplete: (cb: (job: J) => void) => void;
}

type SendEmailJob = Job & {
	recipientEmail: string;
	subject: string;
}

function enqueueJob<T>(job: T): JobRun<T> {
	// queue logic here ....
	return {
		job,
		state: 'queued',
		onComplete: (cb: (job: J) => void) => cb(job)
	};
}

const j: SendEmailJob = {
	recipientEmail: 'bob@bob.com',
	subject: 'bob',
	name: 'email',
	start: () => {},
	state: 'incomplete'
};

const run = enqueueJob(j);

run.onComplete((job) => {
	// job: SendEmailJob
});

```
