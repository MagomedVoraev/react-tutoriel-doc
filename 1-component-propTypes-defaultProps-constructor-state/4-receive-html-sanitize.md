# Recevoir du code HTML et le PURIFY

## Installation de Sanitizer
[DOMPurify](https://github.com/cure53/DOMPurify)

- `yarn add dompurify`
- on l'importe là où on aura le code HTML : `import DOMPurify from 'dompurify';`
- j'écris le code :
```js
import React from 'react';
import PropTypes from 'prop-types';
import DOMPurify from 'dompurify';

const Post = ({
  id, title, category, excerpt,
}) => (
  <article className="post" id={`post-${id}`}>
    <h2 className="post__title">{title}</h2>
    {category ? <div className="post__category">{category}</div> : null}
    <p
      className="post__excerpt"
      // c'est à partir d'ici qu'on l'utilise
      dangerouslySetInnerHTML={{
        __html: DOMPurify.sanitize(
          excerpt,
          {
            ALLOWED_TAGS: [
              'em', 'strong',
            ],
          },
        ),
      }}
    />
  </article>
);

Post.propTypes = {
  id: PropTypes.number.isRequired,
  title: PropTypes.string.isRequired,
  excerpt: PropTypes.string.isRequired,
  category: PropTypes.string,
};

Post.defaultProps = {
  category: null,
};

export default Post;
```

