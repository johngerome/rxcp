<script>
  import AuthUserAvatar from '@pattern/atoms/avatar/AuthUserAvatar.svelte';
  import { createPopper } from '@popperjs/core';
  import { onMount } from 'svelte';
  import SignoutMenu from './SignoutMenu.svelte';
  import UserDropdown from './UserDropdown.svelte';
  import UserInfo from './UserInfo.svelte';
  import UserMenu from './UserMenu.svelte';
  import UserMenuItem from './UserMenuItem.svelte';
  import { user } from '@store/auth';

  let isNavShow = false;
  let navPopper = null;

  onMount(() => {
    const button = document.getElementById('avatarButton');
    const dropdown = document.getElementById('userNavDropdown');

    // Dropdown
    button?.addEventListener('click', showMenu);
    navPopper = createPopper(button, dropdown, {
      placement: 'bottom-end',
      modifiers: [
        {
          name: 'offset',
          options: {
            offset: [0, 10],
          },
        },
      ],
    });

    function showMenu() {
      if (!isNavShow) {
        dropdown.removeAttribute('hidden');
        navPopper.update();
      } else {
        dropdown.setAttribute('hidden', '');
      }

      isNavShow = !isNavShow;
    }

    return () => {
      button.removeEventListener('click', showMenu);
      navPopper.destroy();
      navPopper = null;
    };
  });
</script>

<div>
  <AuthUserAvatar />
  <UserDropdown id="userNavDropdown">
    <UserInfo
      name={`${$user.first_name} ${$user.last_name}`}
      email={$user.email}
    />
    <UserMenu>
      <UserMenuItem to="/admin/profile" text="Profile" />
      <UserMenuItem to="/admin/settings" text="Settings" />
    </UserMenu>
    <SignoutMenu />
  </UserDropdown>
</div>
