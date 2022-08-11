# animation-transitions

Fancy way to describe animation loops in a single array coz cache friendly.
This is a lie, all it does is loop over array indices.
You can probably use it for other things.

### Usage

```Rust
#[derive(Clone, PartialEq)]
pub enum PlayerAnimationVariant {
    Idle,
    Rising,
    Falling,
}

impl AnimationLoop for PlayerAnimationVariant {
    fn page(&self) -> (usize, usize) {
        match self {
            PlayerAnimationVariant::Idle => (0, 3),
            PlayerAnimationVariant::Rising => (2, 2),
            PlayerAnimationVariant::Falling => (4, 4),
        }
    }
}

pub trait AnimationTransition {
    fn next_idx(&mut self) -> usize;
    fn transition_variant(&mut self, to: PlayerAnimationVariant);
}

#[derive(Component, AnimationTransitionMacro)]
pub struct PlayerAnimationState {
    #[variant]
    pub variant: PlayerAnimationVariant,
    pub idx: usize,
}

```

![Screen Shot 2022-08-08 at 3 28 21 PM](https://user-images.githubusercontent.com/11029896/183836973-f002f30f-8ac2-4717-8240-b1a9ecb70813.png)

![Screen Shot 2022-08-08 at 3 28 43 PM](https://user-images.githubusercontent.com/11029896/183836987-f1f6dce6-871e-4e5a-8da3-841734043c46.png)
