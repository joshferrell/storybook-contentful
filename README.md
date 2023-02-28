# Storybook Contentful

A CLI to sync Contentful CMS with Storybook stories. This is useful so that designers can manage the content of storybook using a CMS and not having to contribute to git or the codebase directly.

## Getting started

This project assumes that you are using Storybook and are using mdx for documentation. It's recommended to use Storybook 7 and [Component Story Format 3](https://storybook.js.org/blog/storybook-csf3-is-here/). for best results.

The best structure for your stories is something like this:

```ts
// Button.stories.ts

import type { Meta } from "@storybook/react";
import { Button } from "./Button";

const meta = {
  title: "Button",
  component: Button,
  tags: ["autodocs"],
} satisfies Meta<typeof Button>;

export default meta;

type Story = StoryObj<typeof meta>;

export const Primary: Story = {
  args: {
    primary: true,
    label: "Button",
  },
};
```

```mdx
{/* Button.mdx */}

import { Meta, Story } from "@storybook/blocks";
import * as ButtonStories from "./Button.stories";

<Meta of={ButtonStories} />

# Button

Button is a clickable interactive element.

## Usage

<Story of={ButtonStories.Primary} />
```

### Installation

```bash
pnpm i -D @saasy/storybook-contenful
```

Add the following secrets to your `.env` file. If you're not sure where this information comes from [view the Contenful documentation](https://www.contentful.com/developers/docs/references/authentication/#api-keys-in-the-contentful-web-app) to find these keys and generate them.

```bash
CONTENTFUL_ACCESS_TOKEN=supersecret
CONTENTFUL_SPACE_ID=notsosecret
CONTENTFUL_ENVIRONMENT=master
```

### Usage

Download all files from Contentful and place them in a given path

```bash
storybook-contentful download ./stories
```

Upload all files from the given path to Contentful

```bash
storybook-contentful upload ./stories
```
