# Artisan

**Class based command:**

```php
<?php

namespace App\Console\Commands;

use App\DripEmailer;
use App\User;
use Illuminate\Console\Command;

class SendEmails extends Command
{
  protected $signature = 'email:send {user}';
  
  protected $description = 'Send drip emails to a user';
  
  public function __construct()
  {
    parent::__construct();
  }
  
  public function handle(DripEmailer $drip)
  {
    $drip->send(User::find($this->argument('user')));
  }
}
```

**Closure based command:**

```php
Artisan::command('email:send {user}', function (DripEmailer $drip, $user) {
  $drip->send(User::find($user));
})->describe('Send drip emails to a user');
```

## Defining input expectations

**Arguments:**

```php
// Required argument
$signature = 'email:send {user}';

// Optional argument
$signature = 'email:send {user?}';

// Optional argument with default value
$signature = 'email:send {user=John}';

// Array argument
$signature = 'email:send {user*}';
```

**Options**:

```php
// Switch option
$signature = 'email:send {user} {--queue}';

// Option that receives a value
$signature = 'email:send {user} {--queue=}';

// Option with default value
$signature = 'email:send {user} {--queue=default}';

// Shortcut
$signature = 'email:send {user} {--Q|queue}';

// Option that receives an array
$signature = 'email:send {user} {--id=*}';
```

**Descriptions:**

```php
$signature = 'email:send
              {user : The ID of the user}
              {--queue= : The name of the queue for the job}';
```

## Command I/O

**Retrieving input:**

```php
public function handle()
{
  $userId = $this->argument('user');
  
  $arguments = $this->arguments();
  
  $queueName = $this->option('queue');
    
  $options = $this->options();
}
```

**Prompting for input:**

```php
public function handle()
{
  $name = $this->ask('What is your name?');
  
  $password = $this->secret('What is the password?');
  
  $shouldContinue = $this->confirm('Do you wish to continue?');
  
  $role = $this->anticipate('What is your role?', ['Admin', 'Editor']);
  
  $email = $this->anticipate('What is your email?', function ($input) {
    // Return auto-completion options...
  });
  
  $mood = $this->choice('How are you?', ['Happy', 'Sad'], $defaultIndex, $maxAttempts, $allowMultipleSelections);
}
```

**Writing output:**

```php
public function handle()
{
  $this->line('Uncolored line');
  
  $this->info('Hello world!');
  
  $this->error('Something went wrong!');
}
```

**Table layouts:**

```php
$headers = ['Name', 'Email'];

$users = App\User::all(['name', 'email'])->toArray();

$this->table($headers, $users);
```

**Progress bars:**

```php
$users = App\User::all();

$bar = $this->output->createProgressBar(count($users));

$bar->start();

foreach ($users as $user) {
  $this->performTask($user);
  
  $bar->advance();
}

$bar->finish();
```

## Programmatically executing commands

**Basic usage:**

```php
$exitCode = Artisan::call('email:send', [
  'user' => 1,
  '--queue' => 'default',
]);
```

**Alternative syntax:**

```php
$exitCode = Artisan::call('email:send 1 --queue=default');
```

**Processing in the background with queue workers:**

```php
Artisan::queue('email:send 1 --queue=default');  
```

**Passing an array:**

```php
Artisan::call('email:send', [
  'user' => 1,
  '--id' => [5, 13],
]);
```

**Passing a boolean:**

```php
Artisan::call('migrate:refresh', [
  '--force' => true,
]);
```

