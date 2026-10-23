<script>
  import {
    Activity, AlertCircle, ArrowRight, Bell, CalendarDays, Check, ChevronDown,
    ClipboardList, Clock3, Glasses, LayoutDashboard, MessageCircle, Plus,
    Search, Settings, ShoppingBag, Users, Wallet
  } from '@lucide/svelte';

  let activeNav = 'Overview';

  const primaryNav = [
    { label: 'Overview', icon: LayoutDashboard },
    { label: 'Patients', icon: Users, count: '2,418' },
    { label: 'Appointments', icon: CalendarDays },
    { label: 'Clinical records', icon: ClipboardList },
    { label: 'Dispensing & orders', icon: Glasses }
  ];

  const workNav = [
    { label: 'Workflows', icon: Activity },
    { label: 'Tasks', icon: Check, count: '8' },
    { label: 'Communications', icon: MessageCircle },
    { label: 'Finance', icon: Wallet },
    { label: 'Reports', icon: ShoppingBag }
  ];

  const metrics = [
    { label: "Today's appointments", value: '24', note: '6 remaining today', icon: CalendarDays },
    { label: 'Patients arrived', value: '08', note: '2 currently waiting', icon: Users },
    { label: 'Open tasks', value: '12', note: '3 need attention', icon: ClipboardList },
    { label: 'Orders to collect', value: '07', note: '2 ready for collection', icon: Glasses }
  ];

  const appointments = [
    { time: '09:30', initials: 'JM', name: 'James Mitchell', detail: 'Routine eye examination · Dr Sarah Reid', status: 'Arrived', style: 'waiting' },
    { time: '10:00', initials: 'EW', name: 'Emily Watson', detail: 'Contact lens check · Dr Sarah Reid', status: 'Confirmed', style: 'confirmed' },
    { time: '10:30', initials: 'AB', name: 'Alexander Brown', detail: 'Spectacle collection · Front desk', status: 'Confirmed', style: 'confirmed' },
    { time: '11:00', initials: 'SC', name: 'Sophie Campbell', detail: 'Dispensing appointment · Emma Clark', status: 'Booked', style: '' }
  ];

  const activities = [
    { icon: Glasses, title: 'Order received', detail: ' — Ray-Ban RX5228 for Olivia Fraser', time: '09:18 · Dispensing' },
    { icon: Users, title: 'New patient registered', detail: ' — Daniel Stewart', time: '09:04 · Reception' },
    { icon: MessageCircle, title: 'Recall message sent', detail: ' — 12-month eye examination reminder', time: '08:52 · Automated' },
    { icon: Check, title: 'Task completed', detail: ' — Verify supplier invoice #INV-2048', time: '08:41 · Accounts' }
  ];

  const tasks = [
    { title: 'Call Mrs Henderson about her repair', meta: 'Due today · Patient follow-up', priority: 'High priority' },
    { title: 'Check delivery for order #ORD-1082', meta: 'Due today · Supplier order', priority: 'Normal' },
    { title: 'Review overdue recall responses', meta: 'Due tomorrow · Patient recalls', priority: 'Normal' }
  ];
</script>

<svelte:head>
  <title>Practice overview · OptiCRM</title>
  <meta name="description" content="A patient-centred workspace for modern optical practices." />
</svelte:head>

<div class="app-shell">
  <aside class="sidebar">
    <a class="brand" href="/" aria-label="OptiCRM home">
      <div class="brand-mark">o</div>
      <div>
        <div class="brand-name">OptiCRM</div>
        <div class="brand-sub">Practice workspace</div>
      </div>
    </a>

    <div class="nav-label">Practice</div>
    <nav class="nav-list" aria-label="Practice navigation">
      {#each primaryNav as item}
        <button class:active={activeNav === item.label} class="nav-link" onclick={() => activeNav = item.label}>
          <svelte:component this={item.icon} size={16} strokeWidth={1.8} />
          <span>{item.label}</span>
          {#if item.count}<span class="nav-count">{item.count}</span>{/if}
        </button>
      {/each}
    </nav>

    <div class="nav-label">Operations</div>
    <nav class="nav-list" aria-label="Operations navigation">
      {#each workNav as item}
        <button class:active={activeNav === item.label} class="nav-link" onclick={() => activeNav = item.label}>
          <svelte:component this={item.icon} size={16} strokeWidth={1.8} />
          <span>{item.label}</span>
          {#if item.count}<span class="nav-count">{item.count}</span>{/if}
        </button>
      {/each}
    </nav>

    <div class="sidebar-bottom">
      <div class="nav-label">Workspace</div>
      <button class="nav-link" onclick={() => activeNav = 'Settings'}><Settings size={16} strokeWidth={1.8} /><span>Settings</span></button>
      <div class="practice-card">
        <strong>Aberdeen Eye Care</strong>
        <span>Independent practice</span>
      </div>
      <div class="profile-mini">
        <div class="avatar-small">SR</div>
        <div><strong>Sarah Reid</strong><span>Practice manager</span></div>
        <ChevronDown size={14} />
      </div>
    </div>
  </aside>

  <main class="main-area">
    <header class="topbar">
      <div class="breadcrumb">Practice <span style="padding: 0 7px">/</span> <strong>{activeNav}</strong></div>
      <div class="top-actions">
        <label class="search-box">
          <Search size={14} />
          <input aria-label="Search patients and records" placeholder="Search patients, records..." />
          <span style="font-size:9px; white-space:nowrap">⌘ K</span>
        </label>
        <button class="icon-button" aria-label="Notifications"><Bell size={15} /></button>
      </div>
    </header>

    <section class="content">
      <div class="page-heading">
        <div>
          <div class="eyebrow">Friday, 23 October 2026</div>
          <h1>Good morning, Sarah</h1>
          <p class="subheading">Here’s what’s happening across your practice today.</p>
        </div>
        <button class="primary-button"><Plus size={15} /> New appointment</button>
      </div>

      <div class="metric-grid">
        {#each metrics as metric}
          <article class="metric-card">
            <div class="metric-top"><span>{metric.label}</span><span class="metric-icon"><svelte:component this={metric.icon} size={16} /></span></div>
            <div class="metric-value">{metric.value}</div>
            <div class="metric-foot">{metric.note}</div>
          </article>
        {/each}
      </div>

      <div class="dashboard-grid">
        <section class="panel">
          <div class="panel-header">
            <div><div class="panel-title">Today's appointments</div><div class="panel-subtitle">Your practice schedule · 24 appointments</div></div>
            <a class="text-link" href="/appointments">View calendar <ArrowRight size={12} style="display:inline; vertical-align:middle" /></a>
          </div>
          <div class="appointment-list">
            {#each appointments as appointment}
              <div class="appointment-row">
                <div class="appointment-time">{appointment.time}</div>
                <div class="patient-avatar">{appointment.initials}</div>
                <div><div class="patient-name">{appointment.name}</div><div class="patient-detail">{appointment.detail}</div></div>
                <span class:waiting={appointment.style === 'waiting'} class:confirmed={appointment.style === 'confirmed'} class="status">{appointment.status}</span>
              </div>
            {/each}
          </div>
        </section>

        <section class="panel">
          <div class="panel-header">
            <div><div class="panel-title">Practice activity</div><div class="panel-subtitle">Latest updates across the team</div></div>
            <a class="text-link" href="/activity">View all</a>
          </div>
          <div class="activity-list">
            {#each activities as activity}
              <div class="activity-item">
                <div class="activity-dot"><svelte:component this={activity.icon} size={14} /></div>
                <div class="activity-copy"><strong>{activity.title}</strong>{activity.detail}<div class="activity-time">{activity.time}</div></div>
              </div>
            {/each}
          </div>
        </section>
      </div>

      <div class="lower-grid">
        <section class="panel">
          <div class="panel-header">
            <div><div class="panel-title">My tasks</div><div class="panel-subtitle">Items requiring your attention</div></div>
            <a class="text-link" href="/tasks">All tasks <ArrowRight size={12} style="display:inline; vertical-align:middle" /></a>
          </div>
          <div class="task-list">
            {#each tasks as task}
              <div class="task-row">
                <button class="task-check" aria-label="Mark task complete"></button>
                <div class="task-copy">{task.title}<small>{task.meta}</small></div>
                <span class="priority">{task.priority}</span>
              </div>
            {/each}
          </div>
        </section>

        <section class="panel">
          <div class="panel-header">
            <div><div class="panel-title">Needs attention</div><div class="panel-subtitle">Exceptions worth reviewing</div></div>
            <span class="status waiting">3 alerts</span>
          </div>
          <div class="activity-list">
            <div class="activity-item"><div class="activity-dot" style="background:#fff5e8;color:#ae7b39"><AlertCircle size={14} /></div><div class="activity-copy"><strong>Overdue patient recalls</strong> — 18 patients have not responded to their recall<div class="activity-time">Review suggested · Patient engagement</div></div></div>
            <div class="activity-item"><div class="activity-dot"><Clock3 size={14} /></div><div class="activity-copy"><strong>Unconfirmed appointments</strong> — 4 appointments still need confirmation<div class="activity-time">Today · Reception</div></div></div>
            <div class="activity-item"><div class="activity-dot"><ShoppingBag size={14} /></div><div class="activity-copy"><strong>Supplier order delayed</strong> — Order #ORD-1076 is past its expected date<div class="activity-time">2 days overdue · Dispensing</div></div></div>
          </div>
        </section>
      </div>
    </section>
  </main>
</div>
